---
layout: post
title:  Debug CLION
date:   2021-01-10 11:05:00 +0300
categories: c clion
---
# Как дебажить в clion?
Захотел я сам реализовать простую hashtable на связных списках из [hashtable exercise assigment 7](http://users.cms.caltech.edu/~mvanier/CS11_C/labs/7/lab7.html) и сразу столкнулся с проблемой дебага! Падала у меня программа по segfault и все! Пристальный взгляд,printf не помогали,тут нужен был дебаггер.Мне полному новичку было достаточно тяжело вьехать,как дебажить в Clion.Если в php,еще както привычно,то здесь нет.
**Как я планировал дебажить?**
А с минимальными телодвижениями, есть программа,есть исходник, компилирую с debug символами,хоба и победа!
чтото типа 
```
gcc -g main.c -o main
```
ставлю точку останова и все!Но не помогло,так же не помог Makefile (ну я за полчаса не разобрался,как настроить)
**Как вышло дебажить?**
Пришлось собирать проект с помощью CMake. Это надстройка над  Make которая геренирует Makefile, и CLion ее быстро подхватывает.

## Дебаг
Итак,что у нас есть для дебага, 3 файла test_hash.c,hashtable.c,hashtable.h.
test_hash.c где я пытаюсь реализовать хештаблицу,hashtable.c и hashtable.h => реализация и заголовочные файлы.  ![](https://i.imgur.com/UI8QKRx.png)

Остается их както собрать с помощью CMake.Cам CMakeLists.txt
```
cmake_minimum_required(VERSION 3.17)
project(hashtable)

set(SOURCE_FILES test_hash.c hash_table.c hash_table.h)
add_executable(test ${SOURCE_FILES})
```
Во второй строчке называем проект => **project(hashtable)**, 4 строка устанавливаем переменную **SOURCE_FILES** в которой аж 3 файла, c помощью add_executable обзываем выходной исполняемый файл и все.Остальное у меня CLion сам подхватил
![Дебаггер](https://i.imgur.com/zdv5efI.png)
