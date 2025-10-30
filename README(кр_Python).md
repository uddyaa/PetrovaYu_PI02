def bucket_sort(arr):
    # Создаем 10 корзин
    buckets = [[] for _ in range(10)]

    # Распределяем элементы по корзинам
    for num in arr:
        index = int(num * 10)  # определяем индекс корзины
        buckets[index].append(num)

    # Сортируем каждую корзину
    for bucket in buckets:
        bucket.sort()

    # Объединяем отсортированные корзины
    sorted_arr = []
    for bucket in buckets:
        sorted_arr.extend(bucket)

    return sorted_arr

# Пример
arr = [0.78, 0.17, 0.39, 0.26, 0.72, 0.94, 0.21, 0.12, 0.23, 0.68]
print(bucket_sort(arr))

//Вывод
//[0.12, 0.17, 0.21, 0.23, 0.26, 0.39, 0.68, 0.72, 0.78, 0.94]


def pancake_sort(arr):
    n = len(arr)
    # Проходим по всем элементам массива
    for i in range(n):
        # Находим индекс максимального элемента в текущем диапазоне
        max_idx = 0
        for j in range(1, n - i):
            if arr[j] > arr[max_idx]:
                max_idx = j
        # Если максимум не на месте, поднимаем его к вершине (переворачиваем)
        if max_idx != n - i - 1:
            # Переворачиваем массив до max_idx
            arr[:max_idx + 1] = arr[:max_idx + 1][::-1]
            # Переворачиваем весь текущий диапазон, чтобы переместить максимум на свою позицию
            arr[:n - i] = arr[:n - i][::-1]
    return arr

# Пример использования
arr = [3, 6, 2, 8, 5, 1]
print("Отсортированный массив:", pancake_sort(arr))

//Вывод
//Отсортированный массив: [1, 2, 3, 5, 6, 8]

def bead_sort(arr):
    """Сортировка бусинами (имитирует физический процесс пузырьковой сортировки)."""
    # Находим максимум, чтобы знать высоту "бусин"
    max_val = max(arr)
    # Создаем матрицу "бусин" размером max_val x len(arr)
    beads = [[0]*len(arr) for _ in range(max_val)]
    
    # Размещение бусин: для каждого элемента ставим бусины в соответствующие уровни
    for i in range(len(arr)):
        for j in range(arr[i]):
            beads[j][i] = 1  # бусина есть
    # "Сортируем" бусины: "опускаем" бусины вниз (по строкам)
    for row in beads:
        row.sort()
    # Восстанавливаем отсортированный массив
    for i in range(len(arr)):
        count = 0
        for j in range(max_val):
            if beads[j][i] == 1:
                count += 1
        arr[i] = count
    return arr

# пример
numbers = [5, 3, 1, 7, 4]
print("До сортировки:", numbers)
sorted_numbers = bead_sort(numbers)
print("После сортировки:", sorted_numbers)

//Вывод
//До сортировки: [5, 3, 1, 7, 4]
//После сортировки: [1, 3, 4, 5, 7]


import math

def jump_search(arr, x):
    n = len(arr)
    # Размер шага - примерно √n
    step = int(math.sqrt(n))
    
    # Начинаем прыгать вперед по блокам
    prev = 0
    while prev < n and arr[min(prev + step, n) - 1] < x:
        prev += step
    
    # Линейный поиск внутри блока
    for i in range(prev, min(prev + step, n)):
        if arr[i] == x:
            return i
    return -1  # если элемент не найден

# Пример использования
arr = [1, 3, 5, 7, 9, 11, 13, 15]
target = 11
index = jump_search(arr, target)

if index != -1:
    print(f"Элемент {target} найден на позиции {index}")
else:
    print(f"Элемент {target} не найден")

//Вывод
//Элемент 11 найден на позиции 5


def binary_search(arr, low, high, x):
    while low <= high:
        mid = low + (high - low) // 2
        if arr[mid] == x:
            return mid
        elif arr[mid] < x:
            low = mid + 1
        else:
            high = mid - 1
    return -1

def exponential_search(arr, x):
    n = len(arr)
    if n == 0:
        return -1
    # Проверка первого элемента
    if arr[0] == x:
        return 0
    # Экспоненциальный рост индекса
    index = 1
    while index < n and arr[index] <= x:
        index *= 2
    # Вызов бинарного поиска в обнаруженном диапазоне
    low = index // 2
    high = min(index, n - 1)
    return binary_search(arr, low, high, x)

# Пример использования
arr = [1, 3, 4, 6, 8, 10, 15, 20, 25, 30]
target = 15

result = exponential_search(arr, target)
if result != -1:
    print(f"Элемент {target} найден на позиции {result}")
else:
    print(f"Элемент {target} не найден")

//Вывод
//Элемент 15 найден на позиции 6
