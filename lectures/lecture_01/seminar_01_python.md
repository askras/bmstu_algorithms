---
jupyter:
  jupytext:
    formats: ipynb,md
    text_representation:
      extension: .md
      format_name: markdown
      format_version: '1.3'
      jupytext_version: 1.16.4
  kernelspec:
    display_name: Python 3 (ipykernel)
    language: python
    name: python3
---

<!-- #region editable=true slideshow={"slide_type": ""} -->
# Семинар 1. Введение в программирование на Python

Алгоритмы и структуры данных

МГТУ им. Н.Э. Баумана

Красников Александр Сергеевич

2024
<!-- #endregion -->

<!-- #region editable=true slideshow={"slide_type": ""} -->
## Python файлы
<!-- #endregion -->

<!-- #region editable=true slideshow={"slide_type": ""} -->
- Код на Python обычно хранится в текстовых файлах с расширением "`.py`":

        myprogram.py

- Предполагается, что каждая строка в программном файле Python является оператором Python или его частью. 

  - Единственным исключением являются строки комментариев, которые начинаются с символа #. Строки комментариев обычно игнорируются интерпретатором Python..

- Для запуска нашей программы на Python из командной строки необходимо использовать следующую команду:

        $ python myprogram.py

- В UNIX подобных системах принято указывать путь к интерпретатору в первой строке программы (обратите внимание, что для интерпретатора Pyrhon это строка является комментарием):

        #!/usr/bin/env python

Данная строка получила название *шебанг* (*shebang*)

- Если данная строка является первой строкой в файле, а файл является исполняемым, то можно запустить программу следующим образом:

        $ myprogram.py
<!-- #endregion -->

<!-- #region editable=true slideshow={"slide_type": ""} -->
### Примеры:
<!-- #endregion -->

```python editable=true jupyter={"outputs_hidden": false} slideshow={"slide_type": ""}
ls ./scripts/hello_world*.py
```

```python editable=true jupyter={"outputs_hidden": false} slideshow={"slide_type": ""}
cat ./scripts/hello_world.py
```

```bash editable=true jupyter={"outputs_hidden": false} slideshow={"slide_type": ""}
python ./scripts/hello_world.py
```

```python editable=true slideshow={"slide_type": ""}
!python ./scripts/hello_world_ru.py
```

<!-- #region editable=true slideshow={"slide_type": ""} -->
Обратите внимание, для того чтобы выполнить bash-код в ячейке jupyter notebook необходимо добавить `%%bash` в первой строке ячейки или использовать `!` (восклицательный знак) перед каждой командой оболочки. 

Для многих команд UNIX, например `cat`, `ls`, `pwd` jupyter notebook имеет собственную реализацию перенаправления к оболочке, поэтому использовать `%%bash` или `!` не обязательно.
<!-- #endregion -->

<!-- #region editable=true slideshow={"slide_type": ""} -->
### Кодировка символов
<!-- #endregion -->

<!-- #region editable=true slideshow={"slide_type": ""} -->
Стандартная кодировка символов в файлах Python - UTF-8, но можно использовать любую другую кодировку, например cp1251. 
Чтобы указать, что используется UTF-8, необходимо добавить следующую строку

        # -*- coding: UTF-8 -*-

в начало файла после шебанг строки.

В настоящее время данная строка нужна лишь в случае, использования кодировки отличной от UTF-8. 

        # -*- coding: cp1251 -*-

Но использовать подобные кодировки не рекомендуется.
<!-- #endregion -->

```python editable=true jupyter={"outputs_hidden": false} slideshow={"slide_type": ""}
cat ./scripts/hello_world_ru.py
```

```python editable=true jupyter={"outputs_hidden": false} slideshow={"slide_type": ""}
!python scripts/hello_world_ru.py
```

<!-- #region editable=true slideshow={"slide_type": ""} -->
Кроме этих двух необязательных строк в начале файла кода на Python, для инициализации программы не требуется никакого дополнительного кода.
<!-- #endregion -->

<!-- #region editable=true slideshow={"slide_type": ""} -->
## IPython notebooks
<!-- #endregion -->

<!-- #region editable=true slideshow={"slide_type": ""} -->
Этот файл - тетрадка IPython - не соответствует стандартному шаблону хранения кода Python в текстовом файле. Вместо этого тетрадка IPython хранится в виде файла в формате JSON. 
Преимущество этого подхода заключается в возможности смешивать форматированный текст, код Python и выходные данные кода. 
Для запуска тетрадки IPython требуется сервер IPython notebook, и поэтому она не является автономной программой на Python, как описано выше. 
Кроме этого, нет разницы между кодом на Python, который содержится в программном файле, и кодом на IPython notebook.
<!-- #endregion -->

<!-- #region editable=true slideshow={"slide_type": ""} -->
## Модули
<!-- #endregion -->

<!-- #region editable=true slideshow={"slide_type": ""} -->
Большая часть функциональности в Python обеспечивается *модулями*. 
Стандартная библиотека Python - это большая коллекция модулей, которая обеспечивает *кроссплатформенную* реализацию общих функций, таких как доступ к операционной системе, файловый ввод-вывод, управление строками, сетевое взаимодействие и многое другое.
<!-- #endregion -->

<!-- #region editable=true slideshow={"slide_type": ""} -->
### Ссылки
<!-- #endregion -->

<!-- #region editable=true slideshow={"slide_type": ""} -->
 * The Python Language Reference: http://docs.python.org/2/reference/index.html
 * The Python Standard Library: http://docs.python.org/2/library/
<!-- #endregion -->

<!-- #region editable=true slideshow={"slide_type": ""} -->
Чтобы использовать модуль в программе на Python, его сначала нужно импортировать. 
Модуль можно импортировать с помощью инструкции `import`. 
Например, чтобы импортировать модуль `math`, который содержит множество стандартных математических функций, можно использовать:
<!-- #endregion -->

```python editable=true jupyter={"outputs_hidden": false} slideshow={"slide_type": ""}
import math
```

<!-- #region editable=true slideshow={"slide_type": ""} -->
Эта команда импортирует весь модуль и сделает его доступным для дальнейшего использования в программе. 
Например, можно сделать так:
<!-- #endregion -->

```python editable=true jupyter={"outputs_hidden": false} slideshow={"slide_type": ""}
import math

x = math.cos(2 * math.pi)

print(x)
```

<!-- #region editable=true slideshow={"slide_type": ""} -->
В качестве альтернативы, можно импортировать все сущность (функции и переменные) из модуля в текущее пространство имен. Это позволит не использовать префикс `math.` каждый раз, при использовании элементов модуля:
<!-- #endregion -->

```python editable=true jupyter={"outputs_hidden": false} slideshow={"slide_type": ""}
from math import *

x = cos(2 * pi)

print(x)
```

<!-- #region editable=true slideshow={"slide_type": ""} -->
Этот прием достаточно удобен, но в больших программах, которые включают в себя множество модулей, рекомендуется сохранять сущности из каждого модуля в их собственных пространствах имен, используя строку `import module_name`. 
Это позволит избежать потенциальных проблемы, связанных с конфликтами имен.
<!-- #endregion -->

<!-- #region editable=true slideshow={"slide_type": ""} -->
В качестве третьего варианта, вместо использования подстановочного знака `*`, можно выбрать импорт только нескольких выбранных сущностей из модуля, явно указав, какие из них необходимо импортировать:
<!-- #endregion -->

```python editable=true jupyter={"outputs_hidden": false} slideshow={"slide_type": ""}
from math import cos, pi

x = cos(2 * pi)

print(x)
```

<!-- #region editable=true slideshow={"slide_type": ""} -->
### Просмотр содержимого модуля, и его документации
<!-- #endregion -->

<!-- #region editable=true slideshow={"slide_type": ""} -->
После импортирования модуля становиться возможно просмотреть сущности, которые он предоставляет, используя функцию `dir`:
<!-- #endregion -->

```python editable=true jupyter={"outputs_hidden": false} slideshow={"slide_type": ""}
import math

print(dir(math))
```

<!-- #region editable=true slideshow={"slide_type": ""} -->
Используя функцию `help`, можно получить описание каждой функции (не все функции имеют строки документации, как они называются технически, но подавляющее большинство функций все-таки документированы).
<!-- #endregion -->

```python editable=true jupyter={"outputs_hidden": false} slideshow={"slide_type": ""}
help(math.log)
```

```python editable=true jupyter={"outputs_hidden": false} slideshow={"slide_type": ""}
log(10)
```

```python editable=true jupyter={"outputs_hidden": false} slideshow={"slide_type": ""}
log(10, 2)
```

<!-- #region editable=true slideshow={"slide_type": ""} -->
Можно использовать функцию `help` непосредственно для модуля:
<!-- #endregion -->

```python editable=true slideshow={"slide_type": ""}
help(math)
```

<!-- #region editable=true slideshow={"slide_type": ""} -->
Вот некоторые очень полезные модули из стандартной библиотеки Python: `os`, `sys`, `math`, `shutil`, `re`, `subprocess`, `multiprocessing`, `threading`. 

Полные списки стандартных модулей для Python доступны по адресу http://docs.python.org/3/library/
<!-- #endregion -->

<!-- #region editable=true slideshow={"slide_type": ""} -->
## Переменные и типы
<!-- #endregion -->

<!-- #region editable=true slideshow={"slide_type": ""} -->
### Правила именования
<!-- #endregion -->

<!-- #region editable=true slideshow={"slide_type": ""} -->
Имена переменных в Python могут содержать буквенно-цифровые символы `a-z`, `A-Z`, `0-9` и некоторые специальные символы, такие как `_`. 
Обычные имена переменных должны начинаться с буквы. 

По общему правилу, имена переменных начинаются со строчной буквы, а имена классов - с заглавной. 

Кроме того, существует ряд ключевых слов Python, которые нельзя использовать в качестве имен переменных. К таким ключевым словам относятся:

    and, as, assert, break, class, continue, def, del, elif, else, except, 
    exec, finally, for, from, global, if, import, in, is, lambda, not, or,
    pass, print, raise, return, try, while, with, yield

Примечание: Обратите внимание на ключевое слово `lambda`, которое легко может быть естественным именем переменной в научной программе. 
Но, поскольку это ключевое слово, его нельзя использовать в качестве имени переменной.
<!-- #endregion -->

<!-- #region editable=true slideshow={"slide_type": ""} -->
### Присваивание
<!-- #endregion -->

<!-- #region editable=true slideshow={"slide_type": ""} -->
Оператором присваивания в Python является `=`. 
Python - это язык с динамической типизацией, поэтому нет необходимости указывать тип переменной при ее создании.

Присвоение значения новой переменной создает переменную:
<!-- #endregion -->

```python editable=true jupyter={"outputs_hidden": false} slideshow={"slide_type": ""}
x = 1.0
my_variable = 12.2
```

<!-- #region editable=true slideshow={"slide_type": ""} -->
Тип переменной является производным от значения, которое ей было присвоено.
<!-- #endregion -->

```python editable=true jupyter={"outputs_hidden": false} slideshow={"slide_type": ""}
type(x)
```

<!-- #region editable=true slideshow={"slide_type": ""} -->
Если присвоить переменной новое значение, ее тип может измениться.
<!-- #endregion -->

```python editable=true jupyter={"outputs_hidden": false} slideshow={"slide_type": ""}
x = 1
```

```python editable=true jupyter={"outputs_hidden": false} slideshow={"slide_type": ""}
type(x)
```

<!-- #region editable=true slideshow={"slide_type": ""} -->
При попытке использовать переменную, которая еще не была определена, будет получено сообщение (выбрашено исключение) `NameError`:
<!-- #endregion -->

```python editable=true jupyter={"outputs_hidden": false} slideshow={"slide_type": ""}
print(y)
```

<!-- #region editable=true slideshow={"slide_type": ""} -->
### Простые типы
<!-- #endregion -->

```python editable=true jupyter={"outputs_hidden": false} slideshow={"slide_type": ""}
# Целочисленный тип integer
x = 1
type(x)
```

```python editable=true jupyter={"outputs_hidden": false} slideshow={"slide_type": ""}
# Вещественный тип float
x = 1.0
type(x)
```

```python editable=true jupyter={"outputs_hidden": false} slideshow={"slide_type": ""}
# Логический тип boolean (на самом деле особый случай integer)
b1 = True
b2 = False

type(b1)
```

```python editable=true jupyter={"outputs_hidden": false} slideshow={"slide_type": ""}
# комплексные числа complex
# обратите внимание на использование буквы "j" для указания мнимой части
x = 1.0 - 1.0j
type(x)
```

```python jupyter={"outputs_hidden": false}
print(x)
```

```python jupyter={"outputs_hidden": false}
print(x.real, x.imag)
```

### Функции для проверки типов


Модуль `types` содержит ряд определений имен типов, которые можно использовать для проверки принадлежности переменных к определенным типам

```python jupyter={"outputs_hidden": false}
import types

# печать всех типов, определенных в модуле types
print(dir(types))
```

```python jupyter={"outputs_hidden": false}
x = 1.0

# проверка что переменная x имеет тип float
type(x) is float
```

```python jupyter={"outputs_hidden": false}
# проверка что переменная x имеет тип int
type(x) is int
```

Также для проверки типов переменных можно использовать метод `isinstance`:

```python jupyter={"outputs_hidden": false}
isinstance(x, float)
```

### Приведение типов

```python jupyter={"outputs_hidden": false}
x = 1.5

print(x, type(x))
```

```python jupyter={"outputs_hidden": false}
x = int(x)

print(x, type(x))
```

```python jupyter={"outputs_hidden": false}
z = complex(x)

print(z, type(z))
```

```python jupyter={"outputs_hidden": false}
x = float(z)
```

Комплексные переменные нельзя преобразовать в числа с плавающей запятой или целые числа.
Так как это более «узкие» типы.
Можно использовать `z.real` или `z.imag`, чтобы извлечь нужную часть комплексного числа:

```python jupyter={"outputs_hidden": false}
y = bool(z.real)

print(z.real, " -> ", y, type(y))

y = bool(z.imag)

print(z.imag, " -> ", y, type(y))
```

## Операторы


Большинство операторов в Python работают предсказуемо:

**Арифметические операторы**: 
`+`, `-`, `*`, `/`, `//` (целочисленное деление), `**` (возведение в степень), `%` (взятие остатка от деления) 


```python jupyter={"outputs_hidden": false}
1 + 2, 1 - 2, 1 * 2, 1 / 2
```

```python jupyter={"outputs_hidden": false}
1.0 + 2.0, 1.0 - 2.0, 1.0 * 2.0, 1.0 / 2.0
```

```python jupyter={"outputs_hidden": false}
# Целочисленное деление для вешщественных чисел
3.0 // 2.0
```

```python jupyter={"outputs_hidden": false}
# Внимание! Оператор возведения в степеть в python не ^, а **
2 ** 2
```

Внимание: Оператор `/` всегда возвращает вещественный (float) результат

```python
x = 4
y = 2
z = x / y
print(type(x), type(y), type(z))
```

- для **логических операторов** используются слова `and`, `not`, `or`. 

```python jupyter={"outputs_hidden": false}
True and False
```

```python jupyter={"outputs_hidden": false}
not False
```

```python jupyter={"outputs_hidden": false}
True or False
```

- **Операторы сравнения** `>`, `<`, `>=`, `<=`, `==` (равно), `is` (идентично).

```python jupyter={"outputs_hidden": false}
2 > 1, 2 < 1
```

```python jupyter={"outputs_hidden": false}
2 > 2, 2 < 2
```

```python jupyter={"outputs_hidden": false}
2 >= 2, 2 <= 2
```

```python jupyter={"outputs_hidden": false}
# объекты равны?
[1,2] == [1,2]
```

```python jupyter={"outputs_hidden": false}
# объекты идентичны?
[1,2] is [1,2]
```

```python jupyter={"outputs_hidden": false}
# А эти идентичны?
l1 = l2 = [1,2]

l1 is l2
```

## Составные типы: строки, списки и словари


### Строки


Строки - это тип переменной, который используется для хранения текстовых сообщений.

```python jupyter={"outputs_hidden": false}
s = "Hello world"
type(s)
```

```python jupyter={"outputs_hidden": false}
# Длина строки (количество символов в строке)
len(s)
```

```python jupyter={"outputs_hidden": false}
# Замена подстроки в строке
s2 = s.replace("world", "test")
print(s2)
```

Получить доступ к конкретному символу можно по его индексу (первый символ имеет индек нуль), используя оператор `[]`:

```python jupyter={"outputs_hidden": false}
s[0]
```

Извлечь часть строки можно используя синтаксис `[start:stop]`, который позволяет извлекать символы между индексами `start` и `stop` -1 (символ в индексе `stop` не включается):

```python jupyter={"outputs_hidden": false}
s[0:5]
```

```python jupyter={"outputs_hidden": false}
s[4:5]
```

Если опустить одно из значений (или оба) `start` или `stop` из `[start:stop]`, то по умолчанию будут использоваться начало и конец строки соответственно:

```python jupyter={"outputs_hidden": false}
s[:5]
```

```python jupyter={"outputs_hidden": false}
s[6:]
```

```python jupyter={"outputs_hidden": false}
s[:]
```

Также можно определить размер шага, используя синтаксис `[start:end:step]` (как видно из примеров выше, значение по умолчанию для шага равно 1):

```python jupyter={"outputs_hidden": false}
s[::1]
```

```python jupyter={"outputs_hidden": false}
s[::2]
```

Этот метод называется *срезка* (*slicing*). 
Подробнее смотрите здесь: https://docs.python.org/3/reference/expressions.html#slicings


Python обладает очень богатым набором функций для обработки текста. 
Подробнее смотрие здесь: https://docs.python.org/3/library/string.html


#### Примеры форматирования строк

```python jupyter={"outputs_hidden": false}
# Функция print объединяет строки с помощью пробела
print("str1", "str2", "str3")  
```

```python jupyter={"outputs_hidden": false}
# Функция print преобразуют все аргументы в строки
print("str1", 1.0, False, -1j)  
```

```python jupyter={"outputs_hidden": false}
# строки, добавленные с помощью +, объединяются без пробелов
print("str1" + "str2" + "str3") 
```

```python jupyter={"outputs_hidden": false}
# можно использовать форматирование строк в стиле C
# данный подход считается устаревшим и не рекомендуется к использованию
print("value = %f" % 1.0) 
```

```python jupyter={"outputs_hidden": false}
# при таком форматировании создается строка
s2 = "value1 = %.2f. value2 = %d" % (3.1415, 1.5)

print(s2)
```

```python jupyter={"outputs_hidden": false}
# альтернативный, более интуитивно понятный способ форматирования строки
s3 = 'value1 = {0}, value2 = {1}'.format(3.1415, 1.5)

print(s3)
```

```python
# наиболее современный метод форматирования - f-строки

x = 1
y = 3
z = 1/3

print(f" Если {x} разделить на {y} получим {z:.2f}")
```

### Списки


Списки очень похожи на строки, за исключением того, что каждый элемент списка может быть произвольного типа.

Синтаксис для создания списков в Python следующий `[...]`:

```python jupyter={"outputs_hidden": false}
l = [1,2,3,4]

print(type(l))
print(l)
```

Для работы со списками используются те же методы срезки, что и для работы со строками::

```python jupyter={"outputs_hidden": false}
print(l)

print(l[1:3])

print(l[::2])
```

```python jupyter={"outputs_hidden": false}
l[0]
```

Не обязательно, чтобы все элементы в списке были одного типа:

```python jupyter={"outputs_hidden": false}
l = [1, 'a', 1.0, 1-1j]

print(l)
```

Списки Python могут быть неоднородными и произвольно вложенными:

```python jupyter={"outputs_hidden": false}
nested_list = [1, [2, [3, [4, [5]]]]]

nested_list
```

Списки играют очень важную роль в Python. 
Например, они используются в циклах и других структурах управления потоком (обсуждаемых ниже). Существует ряд удобных функций для создания списков различных типов, например функция `range`:

```python jupyter={"outputs_hidden": false}
start = 10
stop = 30
step = 2

range(start, stop, step)
```

Хотя на самом деле, начиная с python 3 `range` генерирует итератор, который может быть преобразован в список с помощью `list(...)`

```python jupyter={"outputs_hidden": false}
list(range(start, stop, step))
```

```python jupyter={"outputs_hidden": false}
list(range(-10, 10))
```

```python jupyter={"outputs_hidden": false}
s
```

```python jupyter={"outputs_hidden": false}
# преобразование строки в список с помощью приведения типов:
s2 = list(s)

s2
```

```python jupyter={"outputs_hidden": false}
# сортировка списка
s2.sort()

print(s2)
```

#### Добавление, вставка, изменение и удаление элементов из списков

```python jupyter={"outputs_hidden": false}
# создание нового пустого списка
l = []

# для добавления элемента используется `append`
l.append("A")
l.append("d")
l.append("d")

print(l)
```

Списки можно изменять, присваивая новые значения элементам в списке. 
На техническом жаргоне списки являются изменяемыми (*mutable*).

```python jupyter={"outputs_hidden": false}
l[1] = "p"
l[2] = "p"

print(l)
```

```python jupyter={"outputs_hidden": false}
l[1:3] = ["d", "d"]

print(l)
```

Для Вставки элемента по индексу используется `insert`

```python jupyter={"outputs_hidden": false}
l.insert(0, "i")
l.insert(1, "n")
l.insert(2, "s")
l.insert(3, "e")
l.insert(4, "r")
l.insert(5, "t")

print(l)
```

Удалить первый элемент с определенным значением можно, используя `remove`

```python jupyter={"outputs_hidden": false}
l.remove("A")

print(l)
```

Для удаления элемента по индексу используется `del`:

```python jupyter={"outputs_hidden": false}
del l[7]
del l[6]

print(l)
```

Для получения более подробной информации используйте `help(list)`


### Кортежи


Кортежи подобны спискам, за исключением того, что они не могут быть изменены после создания, то есть они являются неизменяемыми (*immutable*). 

В Python кортежи создаются с использованием синтаксиса `(..., ..., ...)`, или даже `..., ...`:

```python jupyter={"outputs_hidden": false}
point = (10, 20)

print(point, type(point))
```

```python jupyter={"outputs_hidden": false}
point = 10, 20

print(point, type(point))
```

Распаковать кортеж можно присвоив его списку переменных, разделенных запятыми:

```python jupyter={"outputs_hidden": false}
x, y = point

print("x =", x)
print("y =", y)
```

Попытка присвоить новое значение элементу кортежа, вызовет исключение:

```python jupyter={"outputs_hidden": false}
point[0] = 20
```

### Словари


Словари также похожи на списки, за исключением того, что каждый элемент представляет собой пару ключ-значение. Синтаксис создания словарей следующий `{key1 : value1, ...}`:

```python jupyter={"outputs_hidden": false}
params = {"parameter1" : 1.0,
          "parameter2" : 2.0,
          "parameter3" : 3.0,}

print(type(params))
print(params)
```

```python jupyter={"outputs_hidden": false}
print("parameter1 = " + str(params["parameter1"]))
print("parameter2 = " + str(params["parameter2"]))
print("parameter3 = " + str(params["parameter3"]))
```

```python jupyter={"outputs_hidden": false}
params["parameter1"] = "A"
params["parameter2"] = "B"

# добавление нового значения
params["parameter4"] = "D"

print("parameter1 = " + str(params["parameter1"]))
print("parameter2 = " + str(params["parameter2"]))
print("parameter3 = " + str(params["parameter3"]))
print("parameter4 = " + str(params["parameter4"]))
```

## Управление потоком


### Условные операторы: if, elif, else


Для условного оператора в Python используются ключевые слова `if`, `elif` (else if), `else`:

```python jupyter={"outputs_hidden": false}
statement1 = False
statement2 = False

if statement1:
    print("statement1 is True")
elif statement2:
    print("statement2 is True")
else:
    print("statement1 and statement2 are False")
```

Здесь мы впервые сталкиваемся со своеобразным и необычным аспектом языка программирования Python: программные блоки определяются уровнем их отступов.

Сравните с эквивалентным кодом на языке C:

    if (statement1)
    {
        printf("statement1 is True\n");
    }
    else if (statement2)
    {
        printf("statement2 is True\n");
    }
    else
    {
        printf("statement1 and statement2 are False\n");
    }

В C блоки вложенности определяются фигурными скобками `{` и `}`. 
И уровень отступа (пробел перед инструкциями кода) не имеет значения. 

А в Python блоки вложенности кода определяются уровнем отступа (обычно это символ табуляции или, скажем, четыре пробела).

Это означает, что нужно быть очень внимательным к отступам, иначе можно получить синтаксические ошибки.


#### Примеры:

```python jupyter={"outputs_hidden": false}
statement1 = statement2 = True

if statement1:
    if statement2:
        print("both statement1 and statement2 are True")
```

```python jupyter={"outputs_hidden": false}
# Неправильные отступы
if statement1:
    if statement2:
    print("both statement1 and statement2 are True")  # эта строка имеет неправильный отступ
```

```python jupyter={"outputs_hidden": false}
statement1 = False 

if statement1:
    print("printed if statement1 is True")
    
    print("still inside the if block")
```

```python jupyter={"outputs_hidden": false}
if statement1:
    print("printed if statement1 is True")
    
print("now outside the if block")
```

## Циклы


В Python циклы могут быть реализованы несколькими различными способами. 
Наиболее распространенным является цикл `for`, который используется совместно с итерируемыми объектами, такими как списки. Основной синтаксис такой:


### Цикл `for`:

```python jupyter={"outputs_hidden": false}
for x in [1,2,3]:
    print(x)
```

Цикл `for` выполняет итерацию по элементам предоставленного списка и выполняет содержащий блок кода один раз для каждого элемента. 
В цикле `for` можно использовать любой тип списка. Например:

```python jupyter={"outputs_hidden": false}
for x in range(4): # по умолчанию range начинается с 0
    print(x)
```

Внимание: `range(4)` не включает 4!

```python jupyter={"outputs_hidden": false}
for x in range(-3,3):
    print(x)
```

```python jupyter={"outputs_hidden": false}
for word in ["Python", "C", "Basic", "Pascal"]:
    print(word)
```

Для перебора пар ключ-значение в словаре:

```python jupyter={"outputs_hidden": false}
for key, value in params.items():
    print(key + " = " + str(value))
```

Иногда бывает полезно иметь доступ к индексам значений при переборе списка. 
Для этого мы можем использовать функцию `enumerate`:

```python jupyter={"outputs_hidden": false}
for idx, x in enumerate(range(-3,3)):
    print(idx, x)
```

### Списковые включения: создание списков используя цикл `for`:


Удобный и компактный способ инициализации списков:

```python jupyter={"outputs_hidden": false}
l1 = [x**2 for x in range(0,5)]

print(l1)
```

### Цикл `while`:

```python jupyter={"outputs_hidden": false}
i = 0

while i < 5:
    print(i)   
    i = i + 1
    
print("done")
```

Обратите внимание, что оператор `print("done")` не является частью тела цикла `while` из-за разницы в отступах.


## Функции


Функция в Python определяется с помощью ключевого слова `def`, за которым следует имя функции, список параметров в круглых скобках `()` и двоеточие `:`. 
Следующий код с одним дополнительным уровнем отступа является телом функции.

```python jupyter={"outputs_hidden": false}
def func0():   
    print("Hello world!")
```

```python jupyter={"outputs_hidden": false}
func0()
```

При создании функций необязательно, но настоятельно рекомендуется определять так называемую "строку документации", которая представляет собой описание назначения и поведения функций. 
Строка документации должна следовать непосредственно после определения функции, перед кодом в теле функции. 

```python jupyter={"outputs_hidden": false}
def func1(s):
    """
    Print a string 's' and tell how many characters it has    
    """
    
    print(s + " has " + str(len(s)) + " characters")
```

```python jupyter={"outputs_hidden": false}
help(func1)
```

```python jupyter={"outputs_hidden": false}
func1("Тест")
```

Функции, возвращающие значение, используют ключевое слово `return`:

```python jupyter={"outputs_hidden": false}
def square(x):
    """
    Return the square of x.
    """
    return x ** 2
```

```python jupyter={"outputs_hidden": false}
square(4)
```

Используя кортеж можно вернуть сразу несколько значений:

```python jupyter={"outputs_hidden": false}
def powers(x):
    """
    Return a few powers of x.
    """
    return x ** 2, x ** 3, x ** 4
```

```python jupyter={"outputs_hidden": false}
powers(3)
```

```python jupyter={"outputs_hidden": false}
x2, x3, x4 = powers(3)

print(x3)
```

### Необязательные и именованные аргументы


При определении функции можно присвоить значения по умолчанию аргументам, которые принимает функция:

```python jupyter={"outputs_hidden": false}
def myfunc(x, p=2, debug=False):
    if debug:
        print("evaluating myfunc for x = " + str(x) + " using exponent p = " + str(p))
    return x**p
```

Если не указывать значение аргумента `debug` при вызове функции `myfunc`, то по умолчанию используется значение, указанное в определении функции:

```python jupyter={"outputs_hidden": false}
myfunc(5)
```

```python jupyter={"outputs_hidden": false}
myfunc(5, debug=True)
```

При вызове функции аргументы не обязательно должны располагаться в том же порядке, что и в определении функции. 
Это называется именованными аргументами и удобно при вызове функций, которые принимают много необязательных аргументов.

```python jupyter={"outputs_hidden": false}
myfunc(p=3, debug=True, x=7)
```

### Анонимные функции (lambda функции)


В Python можно создавать анонимные функции, используя ключевое слово `lambda`:

```python jupyter={"outputs_hidden": false}
# Два эквивалентных способа создания функций

f1 = lambda x: x**2   

def f2(x):
    return x**2
```

```python jupyter={"outputs_hidden": false}
f1(2), f2(2)
```

Этот прием полезен, когда нужно передать простую функцию в качестве аргумента другой функции, например, так:

```python jupyter={"outputs_hidden": false}
# map это встроенная функция Python
list(map(lambda x: x**2, range(-3,4)))
```

## Классы


Классы являются ключевыми элементами объектно-ориентированного программирования. 
Класс - это структура для представления объекта и операций, которые могут выполняться над объектом. 

В Python класс может содержать *атрибуты* (переменные) и *методы* (функции).

Класс определяется почти как функция, но с использованием ключевого слова `class`, и определение класса обычно содержит несколько определений методов класса (функция в классе).

- Каждый метод класса должен иметь аргумент `self` в качестве первого аргумента. Этот объект является ссылкой на самого себя..

- Имена некоторых методов класса имеют особое значение, например:

    - `__init__`: Имя метода, который вызывается при первом создании объекта (конструктор объекта).
    - `__str__` : Метод, который вызывается, когда требуется простое строковое представление класса, например, при печати.
    
https://docs.python.org/3/reference/datamodel.html#special-method-names

```python jupyter={"outputs_hidden": false}
class Point:
    """
    Simple class for representing a point in a Cartesian coordinate system.
    """
    
    def __init__(self, x, y):
        """
        Create a new Point at x, y.
        """
        self.x = x
        self.y = y
        
    def translate(self, dx, dy):
        """
        Translate the point by dx and dy in the x and y direction.
        """
        self.x += dx
        self.y += dy
        
    def __str__(self):
        return("Point at [%f, %f]" % (self.x, self.y))
```

Создание нового экземпляра класса:

```python jupyter={"outputs_hidden": false}
p1 = Point(0, 0) # вызов метода __init__ класса Point

print(p1)         # вызов методв __str__ 
```

```python jupyter={"outputs_hidden": false}
p2 = Point(1, 1)

p1.translate(0.25, 1.5)

print(p1)
print(p2)
```

Обратите внимание, что вызов методов класса может изменять состояние этого конкретного экземпляра класса, но не влияет на другие экземпляры класса или какие-либо глобальные переменные.

Это одна из приятных особенностей объектно-ориентированного проектирования: код, такой как функции и связанные с ними переменные, сгруппирован в отдельные и независимые сущности.


## Модули


Одним из важнейших принципов хорошего программирования является повторное использование кода и избежание повторений.

Идея заключается в написании функций и классов с четко определенной целью и областью применения и их повторном использовании вместо повторения похожего кода в разных частях программы (модульное программирование).
В результате, как правило, значительно улучшается читаемость и удобство обслуживания кода. 

Python поддерживает модульное программирование на разных уровнях. 
Функции и классы являются примерами инструментов для низкоуровневого модульного программирования. 
Модули Python - это высокоуровневая конструкция модульного программирования, в которой можно собирать связанные переменные, функции и классы. 
Модуль в python определяется как отдельный файл python (файл с расширением `.py`), и его можно сделать доступным для других модулей и программ Python, используя инструкцию `import`. 

Рассмотрим следующий пример: файл `mymodule.py` содержит простые примеры реализаций переменной, функции и класса:

```python jupyter={"outputs_hidden": false}
%%file mymodule.py
"""
Example of a python module. Contains a variable called my_variable,
a function called my_function, and a class called MyClass.
"""

my_variable = 0

def my_function():
    """
    Example function
    """
    return my_variable
    
class MyClass:
    """
    Example class.
    """

    def __init__(self):
        self.variable = my_variable
        
    def set_variable(self, new_value):
        """
        Set self.variable to a new value
        """
        self.variable = new_value
        
    def get_variable(self):
        return self.variable
```

Теперь можно импортировать модуль `mymodule` в программу на Python, используя `import`:

```python jupyter={"outputs_hidden": false}
import mymodule
```

Используя `help(module)` для получения информации о модуле:

```python jupyter={"outputs_hidden": false}
help(mymodule)
```

```python jupyter={"outputs_hidden": false}
mymodule.my_variable
```

```python jupyter={"outputs_hidden": false}
mymodule.my_function() 
```

```python jupyter={"outputs_hidden": false}
my_class = mymodule.MyClass() 
my_class.set_variable(10)
my_class.get_variable()
```

При внесении изменений в код `mymodule.py`,  нужно будет перезагрузить его с помощью функцию `reload` из модуля `importlib`:

```python jupyter={"outputs_hidden": false}
from importlib import reload

reload(mymodule)
```

## Исключения


В Python ошибки обрабатываются с помощью специальной языковой конструкции, называемой Исключение (Exception). 
При возникновении ошибок могут быть вызваны исключения, которые прерывают нормальный ход выполнения программы и возвращаются в другое место кода, где определен ближайший оператор `try-except`.


Чтобы сгенерировать исключение, нужно использовать оператор `raise`, принимающий аргумент, который должен быть экземпляром класса `BaseException` или производным от него классом.

```python jupyter={"outputs_hidden": false}
raise Exception("description of the error")
```

Типичным использованием исключений является прерывание работы функций при возникновении какой-либо ошибки, например:

    def my_function(arguments):
    
        if not verify(arguments):
            raise Exception("Invalid arguments")
        
        # rest of the code goes here


Чтобы корректно перехватывать ошибки, генерируемые функциями и методами класса или самим интерпретатором Python, необходимо использовать `try` и `except`:

    try:
        # normal code goes here
    except:
        # code for error handling goes here
        # this code is not executed unless the code
        # above generated an error

Например:

```python jupyter={"outputs_hidden": false}
try:
    print("test")
    # generate an error: the variable test is not defined
    print(test)
except:
    print("Caught an exception")
```

Чтобы получить информацию об ошибке, можно получить доступ к экземпляру класса `Exception`, который описывает исключение. Например:

    except Exception as e:

```python jupyter={"outputs_hidden": false}
try:
    print("test")
    # generate an error: the variable test is not defined
    print(test)
except Exception as e:
    print("Caught an exception:" + str(e))
```

## Смотрите также


- http://www.python.org - Официальный сайт языка программирования Python.
- http://www.python.org/dev/peps/pep-0008 - Руководство по стилю программирования на Python. Настоятельно рекомендуется. 
