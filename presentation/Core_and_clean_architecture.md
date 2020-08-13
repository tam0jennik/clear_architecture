---
marp: true
theme: gaia
_class: lead
paginate: true
backgroundColor: #fff
backgroundImage: url('https://marp.app/assets/hero-background.jpg')
---

![bg left:40% 80%](https://raw.githubusercontent.com/marp-team/marp/master/marp.png)

# **Cap works**

Modern .NET Core and clean architecture

https://marp.app/

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
- disclaimer
- TDD, BDD, DDD, and ETC...
- Onion architecture
- Medator and MediatR, SQRC
- Let's code
- Links to materials
---
# Disclamer
- We don't have a silver bullet
- We don't have a silver bullet
- We don't have a silver bullet
- We don't have a silver bullet

---
# Dad joke story

---
# TDD

---

# DDD
- набор правил, которые позволяют принимать эффективные решения
- основная цель - борьба со сложностью
- ubiquitous language
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
- 

---
## Clean Architecture
domain - enterprise logic and types
application - bussines logic and types
application - specific for this system
domain - specific for this domain
