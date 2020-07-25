---
layout: post
title: JSON query
date: 2020-07-25T00:00:00.000Z
categories: json query jmespath
published: true
---
# JSON query

###### tags: json query jmespath

Иногда возникает задача распарсить JSON,и извлечь оттуда необходимую информацию. Писать код с кучей проверок,условий долго. А если структура JSON чуть поменяется,а если надо выбрать поле по какому-то условию? Прийдется править код.
Облегчают жизнь в этом случае языки запросов к JSON. Например,такой как https://jmespath.org/. 
Предположим, нам надо вытащить количество подписчиков у [therock](https://www.instagram.com/therock/).
Идем по адресу https://www.instagram.com/therock/?__a=1 и видим json типа  (оставил только кусочек json) 
```JSON
{
  logging_page_id: "profilePage_232192182",
  show_suggested_profiles: true,
  show_follow_dialog: false,
  graphql: {
    user: {
      biography: "founder",
      blocked_by_viewer: false,
      restricted_by_viewer: false,
      country_block: false,
      external_url: "http://www.teremana.com/",
      external_url_linkshimmed: "https://l.instagram.com/?u=http%3A%2F%2Fwww.teremana.com%2F&e=ATOFoEJbcrCRyO-hpAa-W52eSf_s01U5hWau7tlY7sRuycdAMdV9xm6pK9WlOiJzIWN_P9xjD1daJllUHoTodw&s=1",
      edge_followed_by: {
        count: 191110623
      },
      followed_by_viewer: false,
      edge_follow: {
        count: 393
      }
    }
  }
}
```
Фолловеры лежат в обьекте **graphql > user > edge_followed_by**  и в свойстве **count**.
Запрос в формате JMES path  на получение подписчиков ,будет выглядеть как
```JSON
graphql.user.edge_followed_by.count
```
т.е. в коде будет что-то типа
```php
$data = json_decode($theRockJsonData);
$pathToFollowers = "graphql.user.edge_followed_by.count";
$followersCount = JmesPath\search($expression, $data);
```
