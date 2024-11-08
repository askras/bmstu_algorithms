<!-- #region editable=true slideshow={"slide_type": ""} -->
## Лабораторная работа № 4 (Cтек, Очередь, Дек)
***Выполнил***: Зейналли С.Р,  ***Группа***: ИУ10-36
<!-- #endregion -->

### **Цель работы** 

Целью данной лабораторной работы является освоение и углубленное понимание динамических структур данных: **стек**, **очередь** и **дек**. В процессе работы студенты познакомятся с ключевыми операциями, выполняемыми с этими структурами, а также научатся их реализовывать в виде классов на основе массивов и связных списков. Реализация этих структур поможет лучше понять принципы работы с памятью, особенности доступа к данным и специфические случаи использования каждой из структур данных. 

Дополнительно в лабораторной работе рассматриваются задачи, такие как проверка сбалансированности скобок и вычисление выражений в постфиксной записи, которые позволяют закрепить теоретические знания на практике.

Данная лабораторная работа посвящена созданию и исследованию структур данных **Стек**, **Очередь** и **Дек** с помощью языков программирования. Основная цель работы — реализовать эти структуры данных в виде классов и применить их для решения различных задач, таких как проверка сбалансированности скобок и вычисление выражений в постфиксной записи.

### 1. Описание задачи

Задача состоит в создании реализаций следующих структур данных:

- **Стек**: структура данных, работающая по принципу "последним пришел — первым вышел" (LIFO).
- **Очередь**: структура данных, работающая по принципу "первым пришел — первым вышел" (FIFO).
- **Дек**: двусторонняя очередь, где добавление и удаление элементов возможно с обоих концов.

Каждая структура данных должна быть реализована двумя способами:
- **На основе массива** — для использования фиксированного количества памяти.
- **На основе связного списка** — для работы с динамическими элементами.

### 2. Входные и выходные данные

**Входные данные**:
- Для **Стеков** и **Очередей**: элементы, которые добавляются или удаляются (числа, строки или символы).
- Для задачи на проверку скобок: строка, состоящая только из символов скобок `(`, `)`, `[`, `]`, `{`, `}`.
- Для задачи на вычисление постфиксного выражения: строка, содержащая цифры и знаки операций (`+`, `-`, `*`, `/`).

**Ожидаемые результаты**:
- Правильная работа всех операций добавления и удаления для каждой структуры данных.
- Вердикт по проверке скобок: сбалансированы ли они или нет.
- Результат вычисления арифметического выражения в постфиксной записи.

### 3. Возможные ограничения и условия решения

- Стек и очередь на основе массива ограничены размером массива, что может потребовать управления переполнением.
- Стек и очередь на основе связного списка не имеют ограничения по количеству элементов, но зависят от доступной памяти.
- Для задачи проверки скобок корректность результата зависит от порядка закрытия всех скобок.
- Выражение в постфиксной записи должно быть корректным для корректного вычисления (например, деление на 0 не допускается).

### 4. Анализ условий решения задачи

- Реализация операций над структурами данных (добавление, удаление, получение текущего элемента) не требует сложных условий, если структуры реализованы правильно.
- Для проверки сбалансированности скобок структура данных **Стек** должна быть корректно реализована, иначе возможны ошибки в последовательности закрытия.
- Для задачи вычисления постфиксного выражения важно наличие двух чисел в стеке перед каждой операцией; иначе выражение будет некорректным и решение невозможно.

### 5. Ожидаемые результаты

Результатом выполнения работы является корректная реализация каждой структуры данных и успешное выполнение дополнительных задач с использованием этих структур. Успешная реализация обеспечит получение правильных ответов для задач на проверку скобок и вычисление выражений, что будет подтверждением корректности работы созданных структур данных.


### Задания на лабораторную работу

#### **1. Реализовать стек на основе массива**


```python
class StackArray:
    def __init__(self):
        self.stack = []

    def is_empty(self) -> int:
        return len(self.stack) == 0

    def push(self, item):
        self.stack.append(item)
        print(f"Added: {item}")

    def pop(self):
        if self.is_empty():
            print("Stack is empty!")
            return None
        return self.stack.pop()

    def peek(self):
        if self.is_empty():
            print("Stack is empty!")
            return None
        return self.stack[-1]

# Тестирование стека на основе массива
stack = StackArray()
stack.push(5)
stack.push(10)
stack.push(30)
print("Peek element:", stack.peek())
print("Deleted:", stack.pop())
print("Peek element after delete:", stack.peek())
```

    Added: 5
    Added: 10
    Added: 30
    Peek element: 30
    Deleted: 30
    Peek element after delete: 10


#### **2. Реализовать стек на основе связного списка**


```python
class Node:
    def __init__(self, value):
        self.value = value
        self.next = None

class StackLinkedList:
    def __init__(self):
        self.head = None

    def is_empty(self):
        return self.head is None

    def push(self, item):
        new_node = Node(item)
        new_node.next = self.head
        self.head = new_node
        print(f"Added: {item}")

    def pop(self):
        if self.is_empty():
            print("Stack is empty!")
            return None
        value = self.head.value
        self.head = self.head.next
        return value

    def peek(self):
        if self.is_empty():
            print("Stack is empty!")
            return None
        return self.head.value

# Тестирование стека на основе связного списка
stack_ll = StackLinkedList()
stack_ll.push(3)
stack_ll.push(7)
stack_ll.push(9)
print("Peek element:", stack_ll.peek())
print("Deleted:", stack_ll.pop())
print("Peek element after delete:", stack_ll.peek())

```

#### **3. Реализовать очередь на основе массива.**



```python
class QueueArray:
    def __init__(self):
        self.queue = []

    def is_empty(self):
        return len(self.queue) == 0

    def enqueue(self, item):
        self.queue.append(item)
        print(f"Added: {item}")

    def dequeue(self):
        if self.is_empty():
            print("Queue is empty!")
            return None
        return self.queue.pop(0)

    def peek(self):
        if self.is_empty():
            print("Queue is empty!")
            return None
        return self.queue[0]

# ### Тестирование очереди на основе массива
queue = QueueArray()
queue.enqueue(3)
queue.enqueue(2)
queue.enqueue(1)
print("Peek element:", queue.peek())
print("Deleted:", queue.dequeue())
print("Peek element after delete:", queue.peek())
```

#### **4. Реализовать очередь на основе связного списка.**


```python
class QueueLinkedList:
    def __init__(self):
        self.head = None
        self.tail = None

    def is_empty(self):
        return self.head is None

    def enqueue(self, item):
        new_node = Node(item)
        if self.tail:
            self.tail.next = new_node
        self.tail = new_node
        if self.head is None:
            self.head = new_node
        print(f"Added: {item}")

    def dequeue(self):
        if self.is_empty():
            print("Queue is empty!")
            return None
        value = self.head.value
        self.head = self.head.next
        if self.head is None:
            self.tail = None
        return value

    def peek(self):
        if self.is_empty():
            print("Queue is empty!")
            return None
        return self.head.value

# ### Тестирование очереди на основе связного списка
queue_ll = QueueLinkedList()
queue_ll.enqueue(3)
queue_ll.enqueue(5)
print("Peek element:", queue_ll.peek())
print("Deleted:", queue_ll.dequeue())
print("Peek element after delete:", queue_ll.peek())
```

#### **5. Реализовать дек на основе массива.**



```python
class DequeArray:
    def __init__(self):
        self.deque = []

    def is_empty(self):
        return len(self.deque) == 0

    def add_front(self, item):
        self.deque.insert(0, item)
        print(f"Added: {item}")

    def add_rear(self, item):
        self.deque.append(item)
        print(f"Added: {item}")

    def remove_front(self):
        if self.is_empty():
            print("Deque is empty!")
            return None
        return self.deque.pop(0)

    def remove_rear(self):
        if self.is_empty():
            print("Deque is empty!")
            return None
        return self.deque.pop()

    def peek_front(self):
        if self.is_empty():
            print("Deque is empty!")
            return None
        return self.deque[0]

    def peek_rear(self):
        if self.is_empty():
            print("Deque is empty!")
            return None
        return self.deque[-1]

# ### Тестирование дека на основе массива
deque = DequeArray()
deque.add_front(4)
deque.add_rear(8)
deque.add_rear(6)
deque.add_front(5)
print("First element:", deque.peek_front())
print("Last element:", deque.peek_rear())
print("Remove front:", deque.remove_front())
print("Remove rear:", deque.remove_rear())
```

    Added: 4
    Added: 8
    Added: 6
    Added: 5
    First element: 5
    Last element: 6
    Remove front: 5
    Remove rear: 6


#### **6. Реализовать дек на основе связного списка**


```python
class Node:
    """Node class for a doubly linked list."""
    def __init__(self, value=None):
        self.value = value
        self.next = None
        self.prev = None

class LinkedListDeque:
    """Implementation of a deque (double-ended queue) using a doubly linked list."""
    def __init__(self):
        self.head = None
        self.tail = None

    def is_empty(self):
        """Check if the deque is empty."""
        return self.head is None

    def add_front(self, value):
        """Add an element to the front of the deque."""
        new_node = Node(value)
        if self.is_empty():
            self.head = self.tail = new_node
        else:
            new_node.next = self.head
            self.head.prev = new_node
            self.head = new_node

    def add_rear(self, value):
        """Add an element to the rear of the deque."""
        new_node = Node(value)
        if self.is_empty():
            self.head = self.tail = new_node
        else:
            new_node.prev = self.tail
            self.tail.next = new_node
            self.tail = new_node

    def remove_front(self):
        """Remove and return the element from the front of the deque."""
        if self.is_empty():
            raise IndexError("Deque is empty")
        value = self.head.value
        self.head = self.head.next
        if self.head is not None:
            self.head.prev = None
        else:
            self.tail = None
        return value

    def remove_rear(self):
        """Remove and return the element from the rear of the deque."""
        if self.is_empty():
            raise IndexError("Deque is empty")
        value = self.tail.value
        self.tail = self.tail.prev
        if self.tail is not None:
            self.tail.next = None
        else:
            self.head = None
        return value

    def peek_front(self):
        """Return the element at the front without removing it."""
        if self.is_empty():
            raise IndexError("Deque is empty")
        return self.head.value

    def peek_rear(self):
        """Return the element at the rear without removing it."""
        if self.is_empty():
            raise IndexError("Deque is empty")
        return self.tail.value


deque = LinkedListDeque()
print("Adding 1 to the front:")
deque.add_front(1)
print("Front element:", deque.peek_front())  

print("Adding 2 to the rear:")
deque.add_rear(2)
print("Rear element:", deque.peek_rear()) 

print("Removing from front:", deque.remove_front()) 
print("Removing from rear:", deque.remove_rear())  

deque.add_front(3)
deque.add_front(4)
deque.add_rear(5)
deque.add_rear(6)

print("Front element after multiple adds:", deque.peek_front())  
print("Rear element after multiple adds:", deque.peek_rear()) 

print("Removing from front:", deque.remove_front()) 
print("Removing from rear:", deque.remove_rear()) 

print("Current front element:", deque.peek_front())  
print("Current rear element:", deque.peek_rear())  

deque.remove_front()
deque.remove_rear()
print("Is deque empty?", deque.is_empty()) 

```

### Дополнительные задания

#### **Задание №1**


```python
def is_balanced_parentheses(expression : str) -> bool:
    stack = StackArray()
    pairs = {')': '(', ']': '[', '}': '{'}
    for char in expression:
        if char in '([{':
            stack.push(char)
        elif char in ')]}':
            if stack.is_empty() or stack.pop() != pairs[char]:
                return False
    return stack.is_empty()

# ### Пример проверки правильности скобок
expression = "{[()]}"
print(f"Скобки в выражении '{expression}' сбалансированы:", is_balanced_parentheses(expression))
```

    Added: {
    Added: [
    Added: (
    Скобки в выражении '{[()]}' сбалансированы: True


#### **Задание №2**


```python
def evaluate_postfix(expression: str) -> int:
    stack = StackArray()
    for char in expression:
        if char.isdigit():
            stack.push(int(char))
        else:
            b = stack.pop()
            a = stack.pop()
            if char == '+':
                stack.push(a + b)
            elif char == '-':
                stack.push(a - b)
            elif char == '*':
                stack.push(a * b)
            elif char == '/':
                stack.push(a / b)
    return stack.pop()

# ### Пример вычисления постфиксного выражения
postfix_expression = "23*54*+"
print(f"Результат вычисления постфиксного выражения '{postfix_expression}':", evaluate_postfix(postfix_expression))
```

    Added: 2
    Added: 3
    Added: 6
    Added: 5
    Added: 4
    Added: 20
    Added: 26
    Результат вычисления постфиксного выражения '23*54*+': 26


### **Контрольные вопросы**

1. **Что такое динамическая структура данных?**
   - Динамическая структура данных — это структура, которая может изменять свой размер во время выполнения программы. Она выделяет память по мере необходимости и освобождает ее, когда данные больше не нужны. Примеры включают связанные списки, деревья и графы.

2. **Что такое стек? Особенности выполнения операций со стеком.**
   - Стек — это линейная структура данных, работающая по принципу "последним пришел — первым вышел" (LIFO). В стеке операции выполняются только с одной стороны, называемой вершиной стека. Основные операции включают добавление элемента (push) и удаление элемента (pop) из вершины стека. Стек используется для временного хранения данных, поддерживает рекурсивные вызовы и управляет вложенностью в вычислениях.

3. **Что такое очередь? Особенности выполнения операций с очередью.**
   - Очередь — это линейная структура данных, работающая по принципу "первым пришел — первым вышел" (FIFO). В очереди добавление элемента происходит с одного конца (задний конец), а удаление — с другого (передний конец). Очередь используется, когда важен порядок обработки данных, например в управлении задачами, обработке запросов или моделировании реальных очередей.

4. **Что такое дек? Особенности выполнения операций с деком.**
   - Дек (двусторонняя очередь) — это структура данных, которая позволяет добавлять и удалять элементы с обоих концов. В отличие от обычной очереди, в деке операции вставки и удаления можно выполнять как с переднего, так и с заднего конца. Это делает дек гибким и подходящим для задач, где требуются доступ и изменения с обеих сторон, например в обработке последовательностей или управлении задачами.

5. **Основные операции со стеком.**
   - **Push:** добавление элемента на вершину стека.
   - **Pop:** удаление и возврат элемента с вершины стека.
   - **Peek (Top):** просмотр элемента на вершине стека без удаления.
   - **isEmpty:** проверка, пуст ли стек. 

