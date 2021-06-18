---
title: "YAML"
tags:
  - doka
authors:
  - KognitivnayaBuena
summary:
  - yaml
  - конфигурация
---

## Кратко

YAML (YAML Ain't Markup Language) - человекопонятный язык для хранения информации. Используется для написания конфигов, чтобы стартовать проект, проверять тесты и для линтеров.
Расширение файла может быть `*.yaml` или `*.yml`- это все YAML.

## Как пишется

Разберём на примере как будет выглядеть вариант конфигурации питомца на YAML. Определим питомцу:

- Имя, которое в последствии лучше заменить на реальное имя любимца.
- Категории его пушистости и возможные звуки которые он издаёт.
- Количество прекрасных лапок.
- Время, которое питомец тратит на обед.

```yaml
bestCatConfiguration:
  # TODO: Вписать имя своего питомца
  name: "insertYourCatName"
  # Тут пример комментария
  isFluffy: true
  sounds:
    - "mur"
    - "pur"
    - "miau"
  paws: 4
  lunchTime: 9.99
```

Для разделения в файле используются отступы — пробелы. Табы не допускаются, потому что иерархия в файле обозначается двойным пробелом. Поэтому лучше настроить себе линтер на проверку и правку. Пара похожа на json и работает по принципу ключ-значение. Определяем ключ и разделяем его со значением символом `:`. После двоеточия следует значение.
В коде можно использовать комментарии. Их определяем через символ `#` и после него пишем текст комментария.

## Структуры данных которые нам доступны в YAML.

### Строки

Можно использовать с кавычками и без, в одно и несколько слов. Все в вашей власти! Ниже примеры:

Без лишних кавычек:

```yaml
name: insertYourCatName
```

Вариант с несколькими словами:

```yaml
name: insert Your Cat Name
```

С использованием двойных или одинарных кавычек (в данном случае двойные):

```yaml
name: "insertYourCatName"
```

### Числа

Можно использовать целые числа значения или с плавающей точкой. Для дробных чисел можно использовать только
точку для разделения, потому что при использовании запятой YAML посчитает значение как строку. Например:

Целое число:

```yaml
paws: 4
```

Число с плавающей точкой:

```yaml
# кот всегда говорит что ему не доложили порцию
lunchTime: 2.99
```

### Списки/массивы

Массивы и списки используют для перечисления данных.
В YAML описывать списки можно двумя способами:

Как массив:

```yaml
sounds: ["mur", "pur", "miau"]
```

Как список:

```yaml
sounds:
  - "mur"
  - "pur"
  - "miau"
```

### Якорь или ссылочная переменная.

Якорь — это приспособление для создания переменных, на которые можно ссылаться. Якорь позволяет вынести повторяющиеся части конфига и использовать ссылку на них в других местах. Так мы можем уменьшить дублирование кода.

Чтобы обозначить якорь используем символ `&`. Чтобы задать значение ссылочной переменной, нужно использовать символ `*`. Символы `<<` показывают что мы просто вставим элементы без привязки к значению ключа.

Зададим базовую конфигурацию питомца с крутым котячьим именем и прекрасным возрастом в два года. Далее прописываем код `<<: *base` в конфигурации. Это означает что мы заполняем поля базовыми значениями. Обращаю внимание на то, что если у нас уже определено поле, то базовая конфигурация туда не пропишется. Следовательно у второго кота будет его гордый возраст в семь лет.

```yaml
base: &base
  name: cool cat name
  age: 2

cat1: &cat1
# Добавляем все значения из base:
  <<: *base

cat2: &cat2
  <<: *base
  # «Перезаписываем» значение для поля `age`:
  age: 7
```

:::callout 📚

Это немного похоже на работу оператора [spread](/js/doka/object/) в JavaScript.

:::

Во что превратится наш код:

```yaml
cat1:
  name: cool cat name
  age: 2

cat2:
  name: cool cat name
  age: 7
```