# Queue

```c#
using System.Collections;
using System.Collections.Generic; // 제네릭 쓰는 경우
```

<br>

---

<br>

#### 선언

```c#
Queue<int> queue = new Queue<int>();
Queue<T> queue = new Queue<T>();
```

<br>

#### 데이터 삽입

```c#
queue.Enqueue(value);
queue.Enqueue(new T());
```

<br>

#### 데이터 확인

```c#
queue.Peek();
```

<br>

#### 데이터 꺼내고 삭제

```c#
int data = queue.Dequeue();
T data = queue.Dequeue();
```

<br>

#### 데이터 비우기

```c#
queue.Clear();
```

<br>

#### 포함한 데이터 갯수 확인

```c#
queue.Count
```

* 비어있는 지 확인할 때 많이 사용