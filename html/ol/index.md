---
title: "`<ol>`"
authors:
  - ezhkov
editors:
  - tachisis
keywords:
  - список
  - упорядоченный список
  - нумерованный список
  - ol
tags:
  - doka
---

## Кратко

Тег упорядоченного списка `<ol>` используется для вёрстки перечня однотипных элементов, когда важен их порядок.

## Пример

```html
<ol>
  <!-- Содержимое -->
</ol>
```

## Как это понять

Тег `<ol>` обозначает начало и конец списка. Сами пункты списка размечаются при помощи тега `<li>`. Таким образом, полностью список размечается с использованием обоих этих тегов:

```html
<ol>
  <li>Первая мировая война</li>
  <li>Вторая мировая война</li>
</ol>
```

Обратите внимание, что дочерними тегами для тега `<ol>` могут быть исключительно теги `<li>` (ещё можно теги `<script>`, но это редкость). Любые другие теги обязательно должны находиться внутри пунктов списка `<li>`. Например, вложенный список должен верстаться так:

```html
<ol>
  <li>Сходить к врачу</li>
  <li>
    Сходить в магазин
    <!-- В этот пункт вложен еще один полноценный список: -->
    <ul>
      <li>Хлеб</li>
      <li>Молоко</li>
    </ul>
  <!-- Закрывающий тег родительского пункта: -->
  </li>
</ol>
```

## Подсказки

💡 Вложенным может быть как неупорядоченный список [`<ul>`](/html/ul), так и упорядоченный список `<ol>`.

```html
<ol>
  <li>Сходить к врачу</li>
  <li>
    Сходить в магазин
    <ul>
      <li>Хлеб</li>
      <li>Молоко</li>
      <li>Сосиски</li>
    </ul>
  </li>
  <li>Приготовить ужин</li>
</ol>
```

💡 Дочерними тегами **обязательно** должны быть `<li>`, в которые уже могут быть вложены любые другие теги.

💡 Как понять, где нужен упорядоченный список: если элементы несут один и тот же смысл, являются частью одной сущности, но явно или неявно подразумевается порядок в перечислении, то выбираем `<ol>`. Пример: план дел на день. Каждое дело — это однотипный элемент, но при этом подразумевается, что дела будут выполнены в определённом порядке.

Бывают ситуации, когда порядок неважен. Например, пункты меню или навигации на сайте. В этом случае выбираем [`<ul>`](/html/ul).
