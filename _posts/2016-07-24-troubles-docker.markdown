---
layout: post
title:  Костыли с докером
date:   2016-07-24 15:05:00 +0300
categories: troubles docker
---
[docker](https://www.docker.com/what-docker) полезная тулза для девелопера.Позволяет создавать и переносить между компами готовый environment,чтоб developer-у не пришлось настраивать,перенастраивать свой рабочий комп.
Этих самых образов в сети полно, и начать пользоватся не так уж сложно. И вот я решив собсвтвенноручно собрать чтото похожее на php-fpm и nginx самому ,а не юзать готовый образ получал ошибку

{%highlight shell%}
*1 FastCGI sent in stderr: "Primary script unknown" while reading response header from upstream,
{%endhighlight%}
Оказалось ,что надо чтоб у этих 2 образов был общий volume.
{% highlight shell %}
cat docker-compose.yml
version: '2'

services:
  nginx:
    build: .
    ports:
      - "8000:80"
    volumes:
       - ./src:/var/www/html
    depends_on:
       - fpm
  fpm:
    image: php:7.0-fpm
    volumes:
        - ./src:/var/www/html

{% endhighlight %}
