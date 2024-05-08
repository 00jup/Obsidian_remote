
# append
```python
def heapSort(arr):
    new_arr = []
    heapConstruct(arr)
    size = len(arr)
    for i in range(0, size):
        new_arr.append(arr.pop(0))
        heapify(arr, 0)
    return new_arr
```

여기서 new_arr.append를 사용해야 한다.
그냥 new_arr[i] = arr.pop(0)을 하게 된다면 list의 크기가 정해지지 않아서 오류가 발생한다.

따라서 new_arr = [None] * size(arr) 혹은 위와 같이 append를 이용하자.


# 코드 전문
```python
## heapSort
def heapConstruct(arr):
    size = len(arr)
    for idx in range(size//2-1, -1, -1):
        heapify(arr, idx)

    return arr

def heapify(arr, idx):
    parent = idx
    l_child = 2*idx + 1
    r_child = 2*idx + 2
    
    if(l_child < len(arr) and arr[l_child]<arr[parent]):
        parent = l_child
    if(r_child < len(arr) and arr[r_child]<arr[parent]):
        parent = r_child
    if(parent != idx):
        arr[idx], arr[parent] = arr[parent], arr[idx]
        heapify(arr, parent)
    
def heapSort(arr):
    new_arr = []
    heapConstruct(arr)
    size = len(arr)
    for i in range(0, size):
        new_arr.append(arr.pop(0))
        heapify(arr, 0)
    return new_arr
```