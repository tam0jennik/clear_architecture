# Добавление нового метода для работы со списком

### 1. Добавим HTTP метод для удаления записи из todo листа
```java 
[HttpDelete("{id}")]
public async Task<ActionResult> Delete(int id)
{
    await Mediator.Send(new DeleteTodoItemCommand { Id = id });

    return NoContent();
}
```
### 2.1. Раскоментируем код фронтенд части:
```Todo.Component.ts```
```javascript
if (!item.title.trim()) {
    this.deleteItem(item);
    return;
}
```
```javascript
// Delete item
deleteItem(item: TodoItemDto) {
    if (this.itemDetailsModalRef) {
        this.itemDetailsModalRef.hide();
    }

    if (item.id == 0) {
        let itemIndex = this.selectedList.items.indexOf(this.selectedItem);
        this.selectedList.items.splice(itemIndex, 1);
    } else {
        this.itemsClient.delete(item.id).subscribe(
            () => this.selectedList.items = this.selectedList.items.filter(t => t.id != item.id),
            error => console.error(error)
        );
    }
}
```

и в файле  `Todo.Component.html`
```html
<button class="btn btn-default text-danger" (click)="deleteItem(selectedItem)">Delete</button>
```

### 2. На слое application создадим каталог для нужного нам юзкейса.
- Назовем его `DeleteTodoItem`
- Создадим команду для удаления элемента

```java
public class DeleteTodoItemCommand : IRequest
{
    public int Id { get; set; }
}
```
- Добавим хендлер для данной операции

```java
public class DeleteTodoItemCommandHandler : IRequestHandler<DeleteTodoItemCommand>
{
    private readonly IApplicationDbContext _context;

    public DeleteTodoItemCommandHandler(IApplicationDbContext context)
    {
        _context = context;
    }

    public async Task<Unit> Handle(DeleteTodoItemCommand request, CancellationToken cancellationToken)
    {
        //ToDo 

        return Unit.Value;
    }
}
```

Мы понимаем что именно нам нужно сделать. Мы выявили все точки и локализовали изменения в коде. Теперь мы можем приступить к написанию тестов. 

### 3. Создадим интеграционный тест для удаления записией из листа.
- для этого в проекте Application.IntegrationTests в каталоге TodoItems.Commands создадим новый класс
 
    ```public class DeleteTodoItemTests : TestBase```
и заимпортируем статический класс - хелпер
    ```using static Testing;```

Я вижу здесь 2 возможных кейса:
- мы пытаемся удалить инвалидный элемент (мы не нашли такое), и хорошо бы чтобы наше приложение могло корректно обработать такой запрос.

```java
[Test]
public void ShouldRequireValidTodoItemId()
{
    var command = new DeleteTodoItemCommand { Id = 99 };

    FluentActions.Invoking(() =>
        SendAsync(command)).Should().Throw<NotFoundException>();
}
```
- и второй момент - это удаление найденного элемента из базы

```java
[Test]
public async Task ShouldDeleteTodoItem()
{
    var listId = await SendAsync(new CreateTodoListCommand
    {
        Title = "New List"
    });

    var itemId = await SendAsync(new CreateTodoItemCommand
    {
        ListId = listId,
        Title = "New Item"
    });

    await SendAsync(new DeleteTodoItemCommand
    {
        Id = itemId
    });

    var list = await FindAsync<TodoItem>(listId);

    list.Should().BeNull();
}
```

### 4. Вернемся к реализации метода удаления элемента и добавим  в него логику.
```java
 public class DeleteTodoItemCommandHandler : IRequestHandler<DeleteTodoItemCommand>
    {
        private readonly IApplicationDbContext _context;

        public DeleteTodoItemCommandHandler(IApplicationDbContext context)
        {
            _context = context;
        }

        public async Task<Unit> Handle(DeleteTodoItemCommand request, CancellationToken cancellationToken)
        {
            var entity = await _context.TodoItems.FindAsync(request.Id);

            if (entity == null)
            {
                throw new NotFoundException(nameof(TodoItem), request.Id);
            }

            _context.TodoItems.Remove(entity);

            await _context.SaveChangesAsync(cancellationToken);

            return Unit.Value;
        }
    }
```

# Создадим middleware для учета времени выполнения методов 
У нас есть реализация и тесты. Тесты зеленые, реализация, возможно, не требует рефакторинга. Давайте воспользуемся одной из интересных возможностей библиотеки медиатр и посчитаем время выполнения методов в продакшен.
для этого ```CleanArchitecture.Application.Common.Behaviours``` добавим ```PerformanceBehaviour.```

```java
public class PerformanceBehaviour<TRequest, TResponse> : IPipelineBehavior<TRequest, TResponse>
    {
        private readonly Stopwatch _timer;
        private readonly ILogger<TRequest> _logger;
        private readonly ICurrentUserService _currentUserService;
        private readonly IIdentityService _identityService;

        public PerformanceBehaviour(
            ILogger<TRequest> logger, 
            ICurrentUserService currentUserService,
            IIdentityService identityService)
        {
            _timer = new Stopwatch();

            _logger = logger;
            _currentUserService = currentUserService;
            _identityService = identityService;
        }

        public async Task<TResponse> Handle(TRequest request, CancellationToken cancellationToken, RequestHandlerDelegate<TResponse> next)
        {
            _timer.Start();

            var response = await next();

            _timer.Stop();

            var elapsedMilliseconds = _timer.ElapsedMilliseconds;

            if (elapsedMilliseconds > 500)
            {
                var requestName = typeof(TRequest).Name;
                var userId = _currentUserService.UserId ?? string.Empty;
                var userName = string.Empty;

                if (!string.IsNullOrEmpty(userId))
                {
                    userName = await _identityService.GetUserNameAsync(userId);
                }

                _logger.LogWarning("CleanArchitecture Long Running Request: {Name} ({ElapsedMilliseconds} milliseconds) {@UserId} {@UserName} {@Request}",
                    requestName, elapsedMilliseconds, userId, userName, request);
            }

            return response;
        }
    }
```
### 6. Зарегистрируем пайплайн в пакете с инджекциями
```CleanArchitecture.Application```

```java
    services.AddTransient(typeof(IPipelineBehavior<,>), typeof(PerformanceBehaviour<,>));
```

