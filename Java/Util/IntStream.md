# IntStream

> `java.util.stream.IntStream`

<br>

---

<br>

```java
int[] num = {88, 55, 99, 57, 83. 26};
int[][] num2 = {
    {88, 55, 99, 57, 83. 26},
    {88, 55, 99, 57, 83. 26},
    {88, 55, 99, 57, 83. 26},
    {88, 55, 99, 57, 83. 26}
}
```

<br>

#### 1. sum

```java
int sum1 = IntStream.of(1,2,3,4,5).sum();
int sum2 = IntStream.of(num).sum();

int sum3 = IntStream.of(num2[0]).sum();
```

<br>

#### 2. max

```java
int max = IntStream.of(num).max();

int max2 = IntStream.of(num2[0]).max();
```

<br>

#### 3. avg

```java
double avg = IntStream.of(num).average().getAsDouble;

double avg2 = IntStream.of(num2[0]).average().getAsDouble;
```

