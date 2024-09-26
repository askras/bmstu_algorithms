---
jupyter:
  jupytext:
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

<!-- #region editable=true slideshow={"slide_type": "slide"} -->
# Лекция 5. Алгоритмы сортировки

Алгоритмы и структуры данных

МГТУ им. Н.Э. Баумана

Красников Александр Сергеевич

2024
<!-- #endregion -->

<!-- #region editable=true slideshow={"slide_type": "subslide"} -->
## План лекции
1. Простейшие методы сортировки
2. Продвинутые методы сортировки
<!-- #endregion -->

<!-- #region editable=true slideshow={"slide_type": "slide"} -->
## Определение

**Сортировка** - процесс упорядочивания данных по возрастанию (убыванию) их значений.


<!-- #endregion -->

<!-- #region editable=true slideshow={"slide_type": "subslide"} -->
### Обмен элементов

Практически во всех методах сортировки есть необходимость обмена местами элементов. 
Этот обмен можно реализовать разными способами.
<!-- #endregion -->

<!-- #region editable=true slideshow={"slide_type": "subslide"} -->
Обычно обмен производится с привлечением дополнительной переменной   
<!-- #endregion -->

```python editable=true slideshow={"slide_type": "fragment"}
a = 3
b = 5

temp = a
a = b
b = temp

print('a =', a, 'b =', b)
```

```python editable=true slideshow={"slide_type": "subslide"}
В Python можно совершить обмен без привлечения дополнительной переменной
```

```python editable=true slideshow={"slide_type": "fragment"}
a = 3
b = 5

a, b = b, a

print('a =', a, 'b =', b)
```

```python editable=true slideshow={"slide_type": "skip"}
Для наглядности и единнобразия создадим функцию `swap` для обмена местами переменных
```

<!-- #region editable=true slideshow={"slide_type": "slide"} -->
## Простейшие методы сортировки

Простейшие методы имеют оценку сложности $O(n^2)$. 
Если n невелико, то такие алгоритмы вполне могут считаться эффективными, благодаря простоте реализации. 
Но с ростом числа элементов будет неизбежно возрастать время сортировки, поэтому при больших n предпочтение нужно отдать более &laquo;продвинутым&raquo; алгоритмам.
<!-- #endregion -->

<!-- #region editable=true slideshow={"slide_type": "subslide"} -->
К простейшим алгоритмам сортировки можно отнести:

- непрактичную сортировку;
- сортировку вставками;
- сортировку выбором;
- пузырьковую сортировку.
<!-- #endregion -->

<!-- #region editable=true slideshow={"slide_type": "slide"} -->
### Непрактичная сортировка (Unratio Sort)

Самой простой для запоминания является непрактичная сортировка.
Сортировка считается непрактичной из-за лишних операций сравнения и обмена (например, arr[0] с arr[0]).
<!-- #endregion -->

```python editable=true slideshow={"slide_type": "subslide"}
def unratio_sort(arr):
    '''Непрактичная сортировка'''
    n = len(arr)
    arr = arr[:]
    for i in range(n):
        for j in range(n):
            if arr[i] < arr[j]:
                arr[i], arr[j] = arr[j], arr[i]
    return arr

# Пример использования
data = [44, 55, 12, 42, 94, 18, 16, 67]
print('Исходный массив данных:', data)
print("Отсортированный массив:", unratio_sort(data))
```

<!-- #region editable=true slideshow={"slide_type": "slide"} -->
### Сортировка вставками (Insertion Sort)

Сортировка вставками  — алгоритм сортировки, в котором элементы входной последовательности просматриваются по одному, и каждый новый поступивший элемент размещается в подходящее место среди ранее упорядоченных элементов

Именно таким образом обычно сортируют карты: держав левой руке уже упорядоченные карты и взяв правой рукой очередную
карту мы вставляем ее в нужное место, сравнивая с уже имеющимися, двигаясь справа налево.
Сортировка вставками удобна для сортировки коротких последовательностей элементов. 

Описание алгоритма:

```
44 \\ 55 12 42 94 18 16 67
44 55 \\ 12 42 94 18 16 67
12 44 55 \\ 42 94 18 16 67
12 42 44 55 \\ 94 18 16 67
12 42 44 55 94 \\ 18 16 67
12 18 42 44 55 94 \\ 16 67
12 16 18 42 44 55 94 \\ 67
12 16 18 42 44 55 67 94 \\
```
<!-- #endregion -->

```python editable=true slideshow={"slide_type": "subslide"}
def insertion_sort(arr):
    '''Сортировка вставками'''
    n = len(arr)
    arr = arr[:]
    for i in range(1, n):
        current_item = arr[i]
        j = i - 1
        while (j >= 0) and (current_item < arr[j]):
            arr[j+1] = arr[j]
            j -= 1
        arr[j+1] = current_item
    return arr

# Пример использования
data = [44, 55, 12, 42, 94, 18, 16, 67]
print('Исходный массив данных:', data)
print("Отсортированный массив:", insertion_sort(data))
```

<!-- #region editable=true slideshow={"slide_type": "slide"} -->
### Сортировка выбором (Selection Sort)

Сортировка выбором – это один из простейших алгоритмов сортировки. 
Он работает по принципу нахождения наименьшего (или наибольшего) элемента в не отсортированной части массива и обмена его с первым элементом не отсортированной части, а затем повторения этой операции для оставшихся элементов.

Описание алгоритма:

1. Начинаем с первого элемента массива (это будет "текущий" элемент).
2. Смотрим на все остальные элементы массива, начиная со второго, ищем наименьший элемент (или наибольший, в зависимости от направления сортировки).
3. После того, как наименьший элемент найден, он меняется местами с текущим элементом.
4. Переходим к следующему элементу и повторяем процесс, пока не отсортируем весь массив.


<!-- #endregion -->

```python editable=true slideshow={"slide_type": "subslide"}
def selection_sort(arr):
    '''Сортировка выбором'''
    n = len(arr)
    arr = arr[:]
    for i in range(n - 1):
        # Предполагаем, что текущий элемент - наименьший
        min_index = i
        for j in range(i + 1, n):
            if arr[j] < arr[min_index]:
                min_index = j
        # Меняем местами найденный наименьший элемент с текущим
        arr[i], arr[min_index] = arr[min_index], arr[i]
    return arr

# Пример использования
data = [44, 55, 12, 42, 94, 18, 16, 67]
print('Исходный массив данных:', data)
print("Отсортированный массив:", selection_sort(data))
```

<!-- #region editable=true slideshow={"slide_type": "slide"} -->
### Пузырьковая сортировка (Bubble Sort)

Для сортировки N-элементного массива методом пузырька требуется до N − 1 проходов. 
В каждом проходе сравниваются соседние элементы, и если, первый из них больше или равен второму, эти элементы меняются местами.

В избыточном варианте циклы выполняются независимо от начального расположения элементов, что ведёт к лишним операциям сравнения, если массив уже упорядочен.
<!-- #endregion -->

```python editable=true slideshow={"slide_type": "subslide"}
def bubble_sort(arr):
    '''Пузырьковая сортировка'''
    n = len(arr)
    arr = arr[:]
    for i in range(n):
        for j in range(n-i-1):
            if arr[j] > arr[j + 1]:
                arr[j], arr[j+1] = arr[j+1], arr[j]
    return arr

# Пример использования
data = [44, 55, 12, 42, 94, 18, 16, 67]
print('Исходный массив данных:', data)
print("Отсортированный массив:", bubble_sort(data))
```

<!-- #region editable=true slideshow={"slide_type": "slide"} -->
### Итоги 

К положительным качествам простейших методов сортировки относят
- экономное расходование памяти
- простота реализации
Главным недостатком сортировок методом вставок, выбора, пузырька является низкая производительность
<!-- #endregion -->

<!-- #region editable=true slideshow={"slide_type": "slide"} -->
## Продвинутые методы сортировки
<!-- #endregion -->

<!-- #region editable=true slideshow={"slide_type": "slide"} -->
### Быстрая сортировка (Quick Sort)

QuickSort - широко известный алгоритм сортировки, разработанный английским учёным Чарльзом Хоаром.
Один из быстрых известных универсальных алгоритмов сортировки массивов, являющийся также, наиболее распространённым.

Краткое описание работы:

- выбрать элемент, называемый опорным
- сравнить все остальные элементы с опорным, на основании сравнения разбить множество на три — меньшие опорного,
равные и большие, расположить их в порядке меньшие-равные-большие.
- повторить рекурсивно для меньших и больших.

<!-- #endregion -->

<!-- #region editable=true slideshow={"slide_type": "subslide"} -->
Достоинства:
- Один из самых быстродействующих (на практике) из алгоритмов внутренней сортировки общего назначения.
- Прост в реализации.
- Требует лишь O(logn) дополнительной памяти для своей работы.
- Хорошо сочетается с механизмами кэширования и виртуальной памяти.

Недостатки:
- Сильно деградирует по скорости (до $O(n^2)$) при неудачных выборах опорных элементов, что может случиться при неудачных входных данных. Этого можно избежать, выбирая опорный элемент случайно, а не фиксированным образом.
- Наивная реализация алгоритма может привести к ошибке переполнения стека, так как ей может потребоваться сделать $O(n)$ вложенных рекурсивных вызовов. В улучшенных реализациях, в которых рекурсивный вызов происходит только для сортировки большей из двух частей массива, глубина рекурсии гарантированно не превысит $O(logn)$.
<!-- #endregion -->

```python editable=true slideshow={"slide_type": "subslide"}

def quick_sort(arr, start, end):
    '''Быстрая сортировка'''
    if end - start > 1:
        p = partition(arr, start, end)
        quick_sort(arr, start, p)
        quick_sort(arr, p + 1, end)
    return(arr)
 
def partition(arr, start, end):
    pivot = arr[start]
    i = start + 1
    j = end - 1
 
    while True:
        while (i <= j and arr[i] <= pivot):
            i = i + 1
        while (i <= j and arr[j] >= pivot):
            j = j - 1
 
        if i <= j:
            arr[i], arr[j] = arr[j], arr[i]
        else:
            arr[start], arr[j] = arr[j], arr[start]
            return j

# Пример использования
data = [44, 55, 12, 42, 94, 18, 16, 67]
print('Исходный массив данных:', data)
print("Отсортированный массив:", quick_sort(data, 0, len(data)))
```

<!-- #region editable=true slideshow={"slide_type": "slide"} -->
### Сортировка Шелла (Shell Sort)

Идея метода заключается в сравнение разделенных на группы элементов последовательности, находящихся друг от друга на некотором расстоянии. 
Изначально это расстояние равно d или N/2, где N — общее число элементов. 
На первом шаге каждая группа включает в себя два элемента расположенных друг от друга на расстоянии N /2; они сравни-
ваются между собой, и, в случае необходимости, меняются местами.
На последующих шагах также происходят проверка и обмен, но расстояние d сокращается на d/2, и количество групп, соответственно, уменьшается.
Постепенно расстояние между элементами уменьшается, и на d=1 проход по массиву происходит в последний раз.
<!-- #endregion -->

```python editable=true slideshow={"slide_type": "subslide"}
def shell_sort(arr):
    '''Сортировка Шелла'''
    n = len(arr)
    arr = arr[:]
    step = len(arr) // 2
    while step > 0:
        for i in range(step, n, 1):
            j = i
            delta = j - step
            while delta >= 0 and arr[delta] > arr[j]:
                arr[delta], arr[j] = arr[j], arr[delta]
                j = delta
                delta = j - step
        step //= 2
    return arr
    
# Пример использования
data = [44, 55, 12, 42, 94, 18, 16, 67]
print('Исходный массив данных:', data)
print("Отсортированный массив:", shell_sort(data))
```

<!-- #region editable=true slideshow={"slide_type": "subslide"} -->
Интересно, но качество данного алгоритма зависит от последовательности значений d.
Существует несколько подходов к выбору этих значений:

1. Первоначально используемая Шеллом последовательность длин промежутков:
d[1] = N/2, d[i] = d[i−1] / 2, d[k] = 1 в худшем случае, сложность алгоритма составит $O(N^2)$
2. Предложенная Хиббардом последовательность: все значения $2^i − 1 \leqslant N$, $i \in N$ такая последовательность шагов приводит к алгоритму сложностью $O(N^{3/2})$
3. Предложенная Седжвиком последовательность:
- $d[i] = 9 \cdot 2^i − 9 \cdot 2^{i/2} + 1$ , если i четное и
- $d[i] = 8 \cdot 2^i − 6 \cdot 2^{(i+1)/2} + 1$ , если i нечетное.
  
При использовании таких приращений средняя сложность алгоритма составляет: $O(n^{7/6})$, а в худшем случае порядка $O(n^{4/3})$.
<!-- #endregion -->

<!-- #region editable=true slideshow={"slide_type": "slide"} -->
###  Сортировка слиянием (Merge Sort)

Слияние означает объединение двух (или более) последовательностей в одну упорядоченную последовательность при помощи циклического выбора элементов, доступных в данный момент.

Сначала задача разбивается на несколько подзадач меньшего размера.
Затем эти задачи решаются с помощью рекурсивного вызова или непосредственно, если их размер достаточно мал. Затем их решения комбинируются, и получается решение исходной задачи.
<!-- #endregion -->

<!-- #region editable=true slideshow={"slide_type": "subslide"} -->
Процедура слияния предполагает объединение двух предварительно упорядоченных подпоследовательностей размерности n/2 в единую последовательность размерности n. 
Начальные элементы предварительно упорядоченных последовательностей сравниваются между собой, и из них выбирается наименьший. 
Соответствующий указатель перемещается на следующий элемент. 
Процедура повторяется до тех пор, пока не достигнут конец одной из подпоследовательностей. 
Оставшиеся элементы другой подпоследовательности при этом передаются в результирующую последовательность в еизменном виде.
<!-- #endregion -->

```python editable=true slideshow={"slide_type": "subslide"}
def merge_sort(arr, left_index, right_index): 
    '''Сортировка слиянием'''
    if left_index >= right_index: 
        return 
 
    middle = (left_index + right_index)//2 
    merge_sort(arr, left_index, middle) 
    merge_sort(arr, middle + 1, right_index) 
    merge(arr, left_index, right_index, middle) 
    
 
     
def merge(arr, left_index, right_index, middle): 
    '''Деление массива на части'''
 
     # Разбиение массива на части
    left_sublist = arr[left_index:middle + 1] 
    right_sublist = arr[middle+1:right_index+1] 
 
    # Переменные для отслеживания положения в каждом подмассиве 
    left_sublist_index = 0 
    right_sublist_index = 0 
    sorted_index = left_index 
 
    # Обход по обеим копиям, пока не закончится один из подмвссивов
    while left_sublist_index < len(left_sublist) and right_sublist_index < len(right_sublist): 
 
        # Если в left_sublist есть элемент меньшего размера, помещаем его в отсортированную часть, 
        if left_sublist[left_sublist_index] <= right_sublist[right_sublist_index]: 
            arr[sorted_index] = left_sublist[left_sublist_index] 
            left_sublist_index = left_sublist_index + 1 
        # Иначе добавляем его в right_sublist 
        else: 
            arr[sorted_index] = right_sublist[right_sublist_index] 
            right_sublist_index = right_sublist_index + 1 
  
        # Продвигаемся вперед по отсортированной части 
        sorted_index = sorted_index + 1 
       
    # Просмотр и добавление оставшихся элементов 
    while left_sublist_index < len(left_sublist): 
        arr[sorted_index] = left_sublist[left_sublist_index] 
        left_sublist_index = left_sublist_index + 1 
        sorted_index = sorted_index + 1 
    while right_sublist_index < len(right_sublist): 
        arr[sorted_index] = right_sublist[right_sublist_index] 
        right_sublist_index = right_sublist_index + 1 
        sorted_index = sorted_index + 1 

# Пример использования
data = [44, 55, 12, 42, 94, 18, 16, 67]
print('Исходный массив данных:', data)
merge_sort(data, 0, len(data))
print("Отсортированный массив:", data)
```
