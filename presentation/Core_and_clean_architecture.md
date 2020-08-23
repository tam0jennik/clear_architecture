---
marp: true
theme: gaia
_class: lead
paginate: true
backgroundColor: #fff
---

![bg left:30% 80%](https://raw.githubusercontent.com/tam0jennik/clear_architecture/master/presentation/img/cap_logo.png)


Modern .NET Core and clean architecture

---

# About me

```java
//Sergei Gladyshev
//Senior full-stack developer 
//Angular+RxJs+net.core
//... 
public void Foo(){
    var joke = "придумать тут шутку, если останется время после подготовки доклада";
    var result = "не осталось, увы";
}
```
---
# Main topics
- Disclaimer
- TDD, DDD, and ETC...
- Onion architecture
- Let's code
- Medator and MediatR, CQRC
- Let's code
- Links to materials
---
# Disclamer
    Часть информации в этом докладе спорная с т.з. академических трудов по архитектуре и пр. 

    Целью доклада было провести краткое погружение в технологии и подходы, которые используются в разработке приложений на net core

<!-- ---

![bg 60%](https://raw.githubusercontent.com/tam0jennik/clear_architecture/master/presentation/img/magnetron.png) -->

---
# TDD
![bg 60%](https://raw.githubusercontent.com/tam0jennik/clear_architecture/master/presentation/img/TDD.png)

---
# TDD
- слабая связанность
- разделение логики на слои
- самоописывающий себя код
---

# DDD
![bg 50%](https://raw.githubusercontent.com/tam0jennik/clear_architecture/master/presentation/img/DDD.png)

---

# DDD
- набор правил, которые позволяют принимать эффективные решения
- основная цель - борьба со сложностью
- ubiquitous language (If you can't explain it simply, you don't understand it well enough)
- bounded context
- с т.з BDD не важно какую архитектуру вы выбререте

---
# DDD
- почти невозможен без чистой архитектуры.
- изменения функциональности должны сохранять кодовую базу чистой
---
## Clean Architecture
- **Domain** all entities, enums, exceptions, interfaces, types and logic specific to the domain layer.
- **Application** all application logic. Dependent only on the domain layer. defines interfaces that are implemented by outside layers. 

- **Infrastructure** contains classes for accessing external resources such as file systems, web services, smtp, and so on.

- **WebUI** SPA, based on Angular 9 and ASP.NET Core 3.1

---
## Clean Arc benefits

- testable
- independent parts
- future-proof
---

## Onion
![bg 60%](https://raw.githubusercontent.com/tam0jennik/clear_architecture/master/presentation/img/Onion.png)

---

## Use cases
![bg 60%](https://raw.githubusercontent.com/tam0jennik/clear_architecture/master/presentation/img/UseCases.png)

---
#### Some words about tests

![bg 60%](https://raw.githubusercontent.com/tam0jennik/clear_architecture/master/presentation/img/UnitTests.png)

---
 
 # let's look at the software
 ![bg 60%]()

---
# CQRS
![bg 60%](https://raw.githubusercontent.com/tam0jennik/clear_architecture/master/presentation/img/sqrs1.png)

---

# CQRS
![bg 60%](https://raw.githubusercontent.com/tam0jennik/clear_architecture/master/presentation/img/sqrs2.png)

---
# MediatR

![bg 60%](https://raw.githubusercontent.com/tam0jennik/clear_architecture/master/presentation/img/mediatr1.png)

---
# MediatR
![bg 90%](https://raw.githubusercontent.com/tam0jennik/clear_architecture/master/presentation/img/mediatr2.png)

---
# Mapping
IMapFrom<>
---
# Validation
---
# Unit of work and Repository
тут нужна картинка
и ключевые описания

---
# Links
- https://github.com/paucls/my-ddd-journey

