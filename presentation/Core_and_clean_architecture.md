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

# About speaker

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
- Medator and MediatR, SQRC
- Let's code
- Links to materials
---
# Disclamer
Часть информации в этом докладе неверная с т.з. академических трудов по архитектуре и пр. 

Целью доклада было провести краткое погружение в технологии и подходы, которые используются в разработке приложений на net core

---
![bg 60%](https://raw.githubusercontent.com/tam0jennik/clear_architecture/master/presentation/img/magnetron.png)

---
# TDD
![bg 60%](https://raw.githubusercontent.com/tam0jennik/clear_architecture/master/presentation/img/TDD.png)

---
# DDD
![bg 50%](https://raw.githubusercontent.com/tam0jennik/clear_architecture/master/presentation/img/DDD.png)

---

# DDD
- набор правил, которые позволяют принимать эффективные решения
- основная цель - борьба со сложностью
- ubiquitous language (Only What You Understand Can You Explain)
- bounded context
- с т.з BDD не важно какую архитектуру вы выбререте, **НО**

---
# DDD
- почти невозможен без чистой архитектуры.
- изменения функциональности должны сохранять кодовую базу чистой
---
### Зачем DDD ?
- код проекта хорошо читается всеми разработчиками, а иногда и аналитиками (ubiquitous language)
- задачи становятся более ясными
- весь проект целиком становится более устойчивым к изменению

---
## Clean Architecture
domain - enterprise logic and types
application - bussines logic and types
application - specific for this system
domain - specific for this domain

---
## Clean benefits

- testable
- independent
---
## Onion
![bg 60%](https://raw.githubusercontent.com/tam0jennik/clear_architecture/master/presentation/img/Onion.png)

---

## Use cases
![bg 60%](https://raw.githubusercontent.com/tam0jennik/clear_architecture/master/presentation/img/UseCases.png)

---
# Domain
- Entities
- Logic
- Exceptions
---
# Application Layer
- Interfaces
- Models
- Logic
- Commands/Queries
- Validators
- Exceptions

---
# CQRS
![bg 60%](https://raw.githubusercontent.com/tam0jennik/clear_architecture/master/presentation/img/sqrs1.png)

---

# CQRS
![bg 60%](https://raw.githubusercontent.com/tam0jennik/clear_architecture/master/presentation/img/sqrs2.png)

---
# MediatR
---
# MediatR

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

