---
layout: post
title: MapReduce
date: '2016-12-15 12:05:00 +0300'
categories: computer science
published: true
---
 иногда просто узнаешь чтото новое =)

# MapReduce
И вот хочу отрекомендовать  статью
[MapReduce](https://static.googleusercontent.com/media/research.google.com/en//archive/mapreduce-osdi04.pdf) за авторством Jeffrey Dean о MapReduce.
Кто такой этот Jeffrey? Это Чак Норрис в разработке софта.

>  Когда Джефф Дин разрабатывает программу, то сначала создаёт бинарник, а потом пишет исходный код как документацию

### Мои впечатления
Cтатья представляет короткий 13 страничный документ.Описывает модель вычислений map-reduce,которая позволяет распараллелить задачи по нескольким машинам.
Пример приведенный в статье, это подсчет числа вхождений слова в текст. Также например распределленный grep(утилита в unix ,которая находит строки отвечающие заданной).

### Пример
Для меня сущность map-reduce заключена в следующем примере. Представим,что вы Санта Клаус,у вас большшшоооой склад с подарками.И вам срочно нужно доставить детям мноого вкусных и непросроченных шоколадок, сосчитать сколько и какие шоколадки есть,и погрузить в мешок.
Вы зовете своих  помощников эльфов и даете  задание каждому:
* Пойдешь на  склад,у тебя по  5 рядов , будешь перебирать все товары на полке,
 если встретишь шоколадку,и она не просрочена напишт на листике ее название.
* Как закончишь,тащите листик ближайшему бригадиру эльфу,
и получай от него следующие 5 рядов. Работать,пока не обойдете весь склад.

Бригадиры тем временем,получает листики с названиями шоколадок,суммируют и отправляют вам отчет.



**Задания которые вы даете эльфам**,и они бегут выполнять **это  map**,а когда эльфам-бригадирам приносят бумажечки с отчетом,и **они суммируют ,это reduce**.

В статье Джефа Дина,также описано как они обеспечивают отказоустойчивость т.е. что делать если ваш worker упал (в контексте данного примера эльф например наелся шоколадок с коньяком и прилег поспать).
Что они делают ,если ваш worker медленно работает( эльф споткнулся о коробку,и захромал,еле ходит)
