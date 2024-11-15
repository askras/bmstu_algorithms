<!-- #region editable=true slideshow={"slide_type": ""} -->
## Лабораторная работа № 5  (Хеш-таблицы и хеш-фукнции)
***Выполнил***: Зейналли С.Р,  ***Группа***: ИУ10-36
<!-- #endregion -->

#### **1. Реализовать хеш-таблицы на основе цепочки.**


```python
from typing import Tuple


class HashNode:
    """Класс для узла хеш-таблицы"""
    def __init__(self, key, value):
        self.key = key
        self.value = value


class HashTable:
    def __init__(self, size = None):  # Уменьшенный размер таблицы для демонстрации коллизий
        """Инициализация хеш-таблицы с указанным размером и пустыми цепочками"""
        self.size = size
        self.table = [[] for _ in range(size)]

    def _hash_function(self, key):
        """Хеш-функция для вычисления индекса"""
        return hash(key) % self.size

    def insert(self, key, value):
        """Добавление элемента в хеш-таблицу"""
        index = self._hash_function(key)
        # Проверка наличия ключа и обновление значения, если ключ уже существует
        for node in self.table[index]:
            if node.key == key:
                node.value = value
                return
        # Если ключ не найден, добавляем новый узел
        self.table[index].append(HashNode(key, value))

    def search(self, key):
        """Поиск значения по ключу"""
        index = self._hash_function(key)
        for node in self.table[index]:
            if node.key == key:
                return node.value
        return None  # Возвращает None, если ключ не найден

    def delete(self, key):
        """Удаление элемента по ключу"""
        index = self._hash_function(key)
        for i, node in enumerate(self.table[index]):
            if node.key == key:
                del self.table[index][i]
                return True
        return False  # Возвращает False, если ключ не найден

    def display(self):
        """Вывод хеш-таблицы"""
        for i, chain in enumerate(self.table):
            print(f"Index {i}: ", end="")
            for node in chain:
                print(f"({node.key}: {node.value})", end=" -> ")
            print("None")


# Пример использования
hash_table = HashTable(size=3)  # Уменьшенный размер таблицы для демонстрации коллизий
hash_table.insert("apple", 1)
hash_table.insert("banana", 2)
hash_table.insert("grape", 3)
hash_table.insert("melon", 4)
hash_table.insert("berry", 5)

# Отображение хеш-таблицы
hash_table.display()

```

    Index 0: (grape: 3) -> None
    Index 1: (apple: 1) -> (melon: 4) -> (berry: 5) -> None
    Index 2: (banana: 2) -> None


#### **2. Реализовать хеш-таблицу на основе открытой адресации.**


```python
from collections import namedtuple

TableEntry = namedtuple('Element', 'hash key value')
class HashTable(object):
    DEFAULT_SIZE = 8
    EMPTY_VALUE = TableEntry(None, None, None)
    DELETED_VALUE = TableEntry(None, None, None)
    LOAD_FACTOR = 2 / 3
    MIN_FACTOR = 1 / 3

    def __init__(self):
        self.container = [self.EMPTY_VALUE] * self.DEFAULT_SIZE
        self.size = 0
        self.deleted_size = 0
        self.container_size = self.DEFAULT_SIZE
    
    def __len__(self):
        return self.size
    
    def __contains__(self, key):
        try:
            _ = self.get(key)
            return True
        except KeyError:
            return False

    def _resize(self):
        old_container = self.container
        old_size = self.size
        self.container_size = int(old_size // self.MIN_FACTOR)
        self.container = [self.EMPTY_VALUE] * self.container_size
        self.size = 0
        self.deleted_size = 0
        for element in old_container:
            if element is not self.EMPTY_VALUE and element is not self.DELETED_VALUE:
                self.set(element.key, element.value)

    def __repr__(self):
        tokens = []
        for element in self.container:
            if element is not self.EMPTY_VALUE and element is not self.DELETED_VALUE:
                tokens.append("{0} : {1}".format(element.key, element.value))
        return "{" + "\n".join(tokens) + "}"

    def _get_entry(self, key):
        """ Return (E0,E1) where E0 is the value or EMPTY_VALUE
        E1 is the index where it was found or if E0 is
        EMPTY_VALUE then the next insert index for the given key
        """
        key_hash = hash(key)
        root_index = key_hash
        for offset in range(self.container_size):
            index = (root_index + offset) % self.container_size
            element = self.container[index]
            if element is self.EMPTY_VALUE \
                or element.hash == key_hash and element.key == key:
                return (element, index)
        raise KeyError

    def set(self, key, value):
        entry, index = self._get_entry(key)
        self.container[index] = TableEntry(hash(key), key, value)
        if entry is self.EMPTY_VALUE:
            self.size += 1
        if (self.deleted_size + self.size) / self.container_size > self.LOAD_FACTOR:
            self._resize()
    
    def __setitem__(self, key, value):
        self.set(key, value)

    def get(self, key):
        entry, _ = self._get_entry(key)
        if entry is self.EMPTY_VALUE:
            raise KeyError('Key {0} not in hash table'.format(key))
        else:
            return entry.value
            
    def __getitem__(self, key):
        return self.get(key)

    def delete(self, key):
        entry, index = self._get_entry(key)
        if entry is self.EMPTY_VALUE:
            raise KeyError('Key {0} not in hash table'.format(key))
        else:
            self.container[index] = self.DELETED_VALUE
            self.size -= 1
            self.deleted_size += 1
    
    def __delitem__(self, key):
        self.delete(key)
        
def test_hash_table():
    hash_table = HashTable()

    # Тест 1: Вставка и получение значений
    print("Тест 1: Вставка и получение значений")
    hash_table.set("apple", 1)
    hash_table.set("banana", 2)
    hash_table.set("cherry", 3)

    print("apple:", hash_table.get("apple"))
    print("banana:", hash_table.get("banana"))
    print("cherry:", hash_table.get("cherry"))
    print()

    # Тест 2: Обновление значения по существующему ключу
    print("Тест 2: Обновление значения")
    hash_table.set("apple", 10)  # Обновление значения
    print("apple (после обновления):", hash_table.get("apple"))
    print()

    # Тест 3: Проверка наличия ключа в таблице
    print("Тест 3: Проверка наличия ключа")
    print("'apple' в таблице:", "apple" in hash_table)
    print("'banana' в таблице:", "banana" in hash_table)
    print("'grape' в таблице:", "grape" in hash_table)
    print()

    # Тест 4: Удаление элемента
    print("Тест 4: Удаление элемента")
    hash_table.delete("apple")
    print("'apple' после удаления:", "apple" in hash_table)
    print("banana после удаления 'apple':", hash_table.get("banana"))
    print()

    # Тест 5: Увеличение размера таблицы при вставке
    print("Тест 5: Увеличение размера таблицы")
    for i in range(10):
        hash_table.set(f"key{i}", i)

    print("Размер таблицы после вставки 10 элементов:", len(hash_table))
    print()

    # Тест 6: Попытка получить несуществующий ключ
    print("Тест 6: Поиск несуществующего ключа")
    try:
        print("get('non_existing_key'):", hash_table.get("non_existing_key"))
    except KeyError:
        print("KeyError: 'non_existing_key' не найден")
    print()

    # Тест 7: Удаление несуществующего ключа
    print("Тест 7: Удаление несуществующего ключа")
    try:
        hash_table.delete("non_existing_key")
    except KeyError:
        print("KeyError: 'non_existing_key' не найден при удалении")
    print()

    # Тест 8: Проверка строкового представления хеш-таблицы
    print("Тест 8: Проверка строкового представления")
    print("Текущее представление хеш-таблицы:", repr(hash_table))
def test_open_addressing():
    hash_table = HashTable()

    # Вставка значений, вызывающих коллизии
    print("Тест 1: Вставка значений с коллизиями")
    keys = ["apple", "banana", "grape", "peach", "plum", "cherry"]
    values = [1, 2, 3, 4, 5, 6]
    for key, value in zip(keys, values):
        hash_table.set(key, value)
        print(f"Вставлен элемент: {key} -> {value}")
        print(f"Текущая хеш-таблица: {hash_table}")
    print("\n")

    # Проверка, что значения были сохранены и найдены корректно
    print("Тест 2: Проверка извлечения значений после коллизий")
    for key in keys:
        print(f"Значение для '{key}':", hash_table.get(key))
    print("\n")

    # Проверка обновления элемента с коллизией
    print("Тест 3: Обновление значения для ключа с коллизией")
    hash_table.set("apple", 10)
    print("Обновлено значение для 'apple': 10")
    print(f"Значение для 'apple' после обновления:", hash_table.get("apple"))
    print(f"Текущая хеш-таблица: {hash_table}")
    print("\n")

    # Проверка удаления элемента, который участвовал в коллизии
    print("Тест 4: Удаление элемента с коллизией")
    hash_table.delete("banana")
    print("Удален элемент 'banana'")
    print(f"Текущая хеш-таблица после удаления 'banana': {hash_table}")
    print("\n")

    # Попытка получить удаленный элемент
    print("Тест 5: Попытка получения удаленного элемента")
    try:
        print("Значение для 'banana':", hash_table.get("banana"))
    except KeyError:
        print("Ошибка: 'banana' не найден, так как был удален")
    print("\n")

    # Вставка нового элемента для проверки переполнения и расширения
    print("Тест 6: Вставка новых элементов для проверки расширения")
    hash_table.set("orange", 7)
    hash_table.set("kiwi", 8)
    hash_table.set("mango", 9)
    print("Вставлены элементы 'orange', 'kiwi', и 'mango'")
    print(f"Текущая хеш-таблица после вставки дополнительных элементов: {hash_table}")
    print("\n")

# Запуск тестов
test_open_addressing()

# Запуск тестов
test_hash_table()
    
```

    Тест 1: Вставка значений с коллизиями
    Вставлен элемент: apple -> 1
    Текущая хеш-таблица: {apple : 1}
    Вставлен элемент: banana -> 2
    Текущая хеш-таблица: {banana : 2
    apple : 1}
    Вставлен элемент: grape -> 3
    Текущая хеш-таблица: {grape : 3
    banana : 2
    apple : 1}
    Вставлен элемент: peach -> 4
    Текущая хеш-таблица: {grape : 3
    banana : 2
    apple : 1
    peach : 4}
    Вставлен элемент: plum -> 5
    Текущая хеш-таблица: {grape : 3
    plum : 5
    banana : 2
    apple : 1
    peach : 4}
    Вставлен элемент: cherry -> 6
    Текущая хеш-таблица: {peach : 4
    cherry : 6
    apple : 1
    plum : 5
    grape : 3
    banana : 2}
    
    
    Тест 2: Проверка извлечения значений после коллизий
    Значение для 'apple': 1
    Значение для 'banana': 2
    Значение для 'grape': 3
    Значение для 'peach': 4
    Значение для 'plum': 5
    Значение для 'cherry': 6
    
    
    Тест 3: Обновление значения для ключа с коллизией
    Обновлено значение для 'apple': 10
    Значение для 'apple' после обновления: 10
    Текущая хеш-таблица: {peach : 4
    cherry : 6
    apple : 10
    plum : 5
    grape : 3
    banana : 2}
    
    
    Тест 4: Удаление элемента с коллизией
    Удален элемент 'banana'
    Текущая хеш-таблица после удаления 'banana': {peach : 4
    cherry : 6
    apple : 10
    plum : 5
    grape : 3}
    
    
    Тест 5: Попытка получения удаленного элемента
    Ошибка: 'banana' не найден, так как был удален
    
    
    Тест 6: Вставка новых элементов для проверки расширения
    Вставлены элементы 'orange', 'kiwi', и 'mango'
    Текущая хеш-таблица после вставки дополнительных элементов: {peach : 4
    mango : 9
    orange : 7
    cherry : 6
    apple : 10
    plum : 5
    kiwi : 8
    grape : 3}
    
    
    Тест 1: Вставка и получение значений
    apple: 1
    banana: 2
    cherry: 3
    
    Тест 2: Обновление значения
    apple (после обновления): 10
    
    Тест 3: Проверка наличия ключа
    'apple' в таблице: True
    'banana' в таблице: True
    'grape' в таблице: False
    
    Тест 4: Удаление элемента
    'apple' после удаления: False
    banana после удаления 'apple': 2
    
    Тест 5: Увеличение размера таблицы
    Размер таблицы после вставки 10 элементов: 12
    
    Тест 6: Поиск несуществующего ключа
    KeyError: 'non_existing_key' не найден
    
    Тест 7: Удаление несуществующего ключа
    KeyError: 'non_existing_key' не найден при удалении
    
    Тест 8: Проверка строкового представления
    Текущее представление хеш-таблицы: {key2 : 2
    key6 : 6
    key0 : 0
    key7 : 7
    cherry : 3
    key4 : 4
    key1 : 1
    key3 : 3
    key8 : 8
    banana : 2
    key9 : 9
    key5 : 5}


#### **3. Блокчейн (2 балла) В блокчейне хеш-функции используются для создания уникальных идентификаторов блоков и обеспечения целостности данных. Каждый блок содержит хеш предыдущего блока, что создает цепочку и делает систему устойчивой к изменениям.**


```python
import hashlib
import time

class Block:
    def __init__(self, index, previous_hash, data, timestamp=None):
        self.index = index
        self.previous_hash = previous_hash
        self.data = data
        self.timestamp = timestamp or time.time()
        self.hash = self.calculate_hash()

    def calculate_hash(self):
        sha = hashlib.sha256()
        sha.update((str(self.index) + str(self.previous_hash) + str(self.data) + str(self.timestamp)).encode('utf-8'))
        return sha.hexdigest()

    def __str__(self):
        return f"Block(Index: {self.index}, Hash: {self.hash}, Previous Hash: {self.previous_hash}, Data: {self.data})"

class Blockchain:
    def __init__(self):
        self.chain = [self.create_genesis_block()]

    def create_genesis_block(self):
        return Block(0, "0", "Genesis Block", time.time())

    def add_block(self, data):
        previous_block = self.chain[-1]
        new_block = Block(len(self.chain), previous_block.hash, data)
        self.chain.append(new_block)

    def is_chain_valid(self):
        for i in range(1, len(self.chain)):
            current_block = self.chain[i]
            previous_block = self.chain[i - 1]

            # Проверка хеша текущего блока
            if current_block.hash != current_block.calculate_hash():
                print(f"Ошибка: Хеш блока {current_block.index} не совпадает.")
                return False
            
            # Проверка хеша предыдущего блока
            if current_block.previous_hash != previous_block.hash:
                print(f"Ошибка: Блок {current_block.index} не ссылается корректно на предыдущий блок.")
                return False
        return True

    def print_chain(self):
        for block in self.chain:
            print(block)

# Пример использования
blockchain = Blockchain()
blockchain.add_block("Первый блок с данными")
blockchain.add_block("Второй блок с данными")

# Вывод цепочки и проверка целостности
blockchain.print_chain()
print("Цепочка валидна:", blockchain.is_chain_valid())

```

    Block(Index: 0, Hash: 5ea8c4959bfc5224e3b7c2ff797436204d7cb4bf68e406fcc70ff109cd084d79, Previous Hash: 0, Data: Genesis Block)
    Block(Index: 1, Hash: 8785dab4d09e927781d7a30a55cb601cc1dfe9b9c851ef1f53afd3e5cd99f8b9, Previous Hash: 5ea8c4959bfc5224e3b7c2ff797436204d7cb4bf68e406fcc70ff109cd084d79, Data: Первый блок с данными)
    Block(Index: 2, Hash: 83849203e6e28d48f737aa319597cea76688e4dc04cc8b8f3384ebbf71c54f7c, Previous Hash: 8785dab4d09e927781d7a30a55cb601cc1dfe9b9c851ef1f53afd3e5cd99f8b9, Data: Второй блок с данными)
    Цепочка валидна: True


#### **4. Проверка пересечения двух массивов (1 балл)**


```python
def has_intersection(first_array: list[int], second_array: list[int]) -> bool: 
    set_first_array = set(first_array)
    for element in second_array:
        if element in set_first_array:
            return True
    return False

A = [1, 2, 3, 4]
B = [4, 5, 6]
print(has_intersection(A, B))
```

    True


#### **5. Проверка уникальности элементов в массиве.**


```python
def has_unique_elements_with_hash(arr):
    element_count = {}
    for element in arr:
        if element in element_count:
            return False
        element_count[element] = True 
    return True 

# Пример использования
arr = [1, 2, 3, 4, 5]
print(has_unique_elements_with_hash(arr)) 

arr_with_duplicates = [1, 2, 3, 4, 2]
print(has_unique_elements_with_hash(arr_with_duplicates)) 

```

    True
    False


#### **6. Нахождение пар с заданной суммой.**


```python
from typing import Any
def twosum(numbers: list[int], target: int) -> tuple[Any, Any] | None:
    number_map = {}
    for i, number in enumerate(numbers):
        diff = target - number
        if diff in number_map:
            return number, diff
        number_map[number] = i
    return None

nums = [2, 7, 11, 15]
target = 9
result = twosum(nums, target)
print(result)  # Выведет (7, 2), так как 7 + 2 = 9

```

    (7, 2)


#### **7. Задача на проверку анаграмм.**


```python
def anagram_check(string: str, text: str) -> bool:
    if len(text) != len(string): return False
    
    count_S, count_T = {}, {}
    
    for i in range(len(string)):
        count_S[string[i]] = count_S.get(string[i], 0) + 1
        count_T[text[i]] = count_T.get(text[i], 0) + 1
    return count_S == count_T

str = "cat"
text = "tac"
print(anagram_check(str, text))
```

    True




---

# Контрольные вопросы по хешированию

## 1. Назначение хеширования

**Хеширование** — это процесс преобразования данных (например, строки, числа, объекта) в уникальный идентификатор фиксированной длины, называемый **хеш-значением** или **хеш-кодом**. Основное назначение хеширования:

- **Ускорение поиска данных**: Хеш-функции позволяют быстро искать, вставлять и удалять элементы в структуре данных (например, хеш-таблице), обеспечивая доступ к данным за время \( O(1) \) в среднем.
- **Проверка целостности данных**: Хеш-функции используются для создания контрольных сумм, позволяя проверить, были ли данные изменены.
- **Шифрование и безопасность**: Хеш-функции играют ключевую роль в алгоритмах криптографии, например, в цифровых подписях и хешировании паролей.

## 2. Способы реализации хеш-функций и хеш-таблиц

### Хеш-функции:
- **Математические хеш-функции**: Преобразуют данные в фиксированное значение с использованием математических операций (например, умножение, деление, битовые сдвиги).
  - Пример: `h(k) = k mod m`, где `k` — это ключ, а `m` — размер таблицы.
  
- **Криптографические хеш-функции**: Специально разработаны для обеспечения безопасности, такие хеш-функции устойчивы к коллизиям и труднообратимы.
  - Примеры: SHA-256, MD5.

- **Действие на строках**: Когда хешируемые данные — это строки, хеш-функции могут использовать сумму ASCII значений символов, умноженную на некоторые константы, или же более сложные методы.
  - Пример: Хеширование строк с использованием алгоритма, основанного на полиномиальной хеш-функции.

### Хеш-таблицы:
- **Простая хеш-таблица**: Массив с фиксированным размером, в котором хеш-коды элементов используются для определения их индексов.
  - При вставке элемента его хеш-код вычисляется и используется для индексации.
  - Преимущество: Быстрый доступ \( O(1) \), если нет коллизий.
  
- **Динамическая хеш-таблица**: Массив с возможностью изменения размера при увеличении количества элементов, что помогает избежать переполнения и улучшить производительность.

## 3. Понятие коллизии

**Коллизия** — это ситуация, когда два различных элемента (например, строки, числа) имеют одинаковое хеш-значение, то есть хеш-функция генерирует одинаковые индексы для разных входных данных. Коллизии могут возникать в любой хеш-таблице, так как пространство возможных хеш-кодов ограничено, а количество возможных данных — нет.

## 4. Варианты разрешения коллизий в хеш-таблице

Для решения коллизий существует несколько популярных методов:

### 1. Открытая адресация (Open Addressing)
При возникновении коллизии система поиска пытается найти следующий свободный слот в таблице для хранения элемента. Это достигается за счет различных стратегий поиска свободных мест:
- **Линейное пробирование**: Если возникает коллизия, проверяется следующий слот, и так до тех пор, пока не будет найден пустой.
- **Квадратичное пробирование**: Слоты проверяются с увеличением шага (например, 1, 4, 9, 16 и так далее).
- **Двойное хеширование**: Используется вторая хеш-функция для вычисления шага, по которому будет производиться поиск.

### 2. Цепочки (Chaining)
Вместо того чтобы искать свободный слот, для каждого индекса таблицы создается связанный список (или другая структура данных). Когда возникает коллизия, элементы, имеющие одинаковое хеш-значение, добавляются в этот список.
- Преимущество: Простота реализации и гибкость, так как количество элементов не ограничено размером хеш-таблицы.
- Недостаток: Время поиска может ухудшиться до \( O(N) \), если все элементы окажутся в одном списке.

### 3. Редиректирование или замена (Rehashing)
Этот метод заключается в том, что при возникновении коллизии хеш-таблица перераспределяет элементы по новой таблице, используя новую хеш-функцию или увеличивая размер таблицы. Это помогает уменьшить вероятность коллизий.

---
