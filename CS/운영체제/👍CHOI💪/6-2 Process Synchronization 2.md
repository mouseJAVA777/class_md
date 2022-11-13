# Process Synchronization 2



### Initial Attempts to Solve Critical-Section Problem

```c
do {
  entry section				// lock
  critical section
  exit section				// unlock
  remainder section
} while (1);
```



### 프로그램적 해결법의 총족 조건

1. Mutual Exclusion (상호 배제)

   : 한 프로세스가 Critical Section 부분을 수행 중이면 다른 프로세스는 해당 Section에 접근하면 안 됨

2. Progress (진행)

   : Critical Section을 수행하는 프로세스가 없다면 해당 Section을 수행하고자하는 프로세스를 접근 허용해주어야 함

3. Bounded Waiting (유한 대기)

   : 하나의 프로세스가 Critical Section에 접근을 요청한 이후 다른 프로세스의 Critical Section에 대한 접근 횟수에 한계가 있어야 함 (Starvation 방지)



### Algorithm 1

Process<sub>0</sub>을 위한 코드

```c
do {
  while (turn != 0);	// 0만 while문 탈출해서 critical section 접근
  critical section
  turn = 1;						// 이제 1만 접근할 수 있도록 업데이트
  remainder section
} while (1);
```

Process<sub>1</sub>을 위한 코드

```c
do {
  while (turn != 1);
  critical section
  turn = 0;
  remainder section
} while (1);
```

*turn : Process의 id 개념*

- Mutual Exclusion ⭕️
- Progress ❌ : 반드시 교대로 들어가야하기 때문



### Algorithm 2

Process<sub>i</sub>을 위한 코드

```c
do {
  flag[i] = true;			// i번째 프로세스가 접근 시도
  while (flag[j]);		// 이미 접근한 프로세스가 있으면 접근 차단
  critical section
  flag[i] = false;		// 이제 다른 프로세스도 다시 접근 가능하도록 업데이트
  remainder section
} while (1);
```

*P<sub>i</sub> ready to enter its critical section if flag[i] == true*

- Mutual Exclusion ⭕️
- Progress ❌ : Process<sub>i</sub>가 flag를 true로 바꾼 직후 Process<sub>j</sub>가 CPU를 얻게 되어 Critical Section에 접근하려 할 때, 둘 다 Critical Section에 접근 불가



### Algorithm 3 (Peterson's Algorithm)

Process<sub>i</sub>을 위한 코드

```c
do {
  flag[i] = true;
  turn = j;
  while (flag[j] && turn == j);
  critical section
  flag[i] = false;
  remainder section
} while (1);
```

Process<sub>j</sub>을 위한 코드

```c
do {
  flag[j] = true;
  turn = i;
  while (flag[i] && turn == i);
  critical section
  flag[j] = false;
  remainder section
} while (1);
```

- Mutual Exclusion ⭕️
- Progress ⭕️
- Bounded Waiting ⭕️
- Busy Waiting (Spin Lock) : 계속 CPU와 메모리를 사용하면서 Wait하는 문제 (비효율의 문제)



### Synchronization Hardware

: 하드웨어적으로 Test & Modify를 Atomic하게 수행할 수 있도록 지원하는 경우 앞의 문제는 간단히 해결 가능

  하나의 Instruction으로 데이터를 읽고 쓰는 작업을 동시에 진행할 수 있다면

```c
Synchronization variable:
	boolean lock = false;

Process Pi
  do {
    while (Test_and_Set(lock));
    critical section
    lock = false;
    remainder section
  }
```

*Test_and_Set(x) : x값을 읽고 x를 true(1)로 바꾸어주는 Instruction*