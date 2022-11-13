# Process Synchronization 3



### Semaphores

: 앞의 방식을 추상화, 일종의 추상자료형

*추상자료형 :  자료들(object)과 그 자료들에 대한 연산(operator)들을 명기한 것으로 구현 방법을 명시하고 있지 않음*

Semaphore S

- 정수형 변수

- 두 가지 Atomic 연산

  - P(S) : 공유 데이터를 획득하는 과정 (S는 자원의 개수) 따라서 S가 양수일 때는 하나씩 줄어들고, 0 이하일 때는 다시 양수가 될 때까지 Wait (Busy-Wait 문제)

    `while (S<=0) do no-op; `

    `S--;`

  - V(S) : 공유 데이터 사용 후 반납하는 과정

    `S++;`



### Critical Section of n Processes

1. Busy-Wait (Spin Lock) : *비효율적*

```c
/*Synchronization variables*/
Semaphore mutex; 		/*initially 1*/

/*Process Pi*/
do {
  P(mutex);					/*decrement only if positive*/
  critical section
  V(mutex);					/*increment*/
  remainder section
} while (1)
```

2. Block & Wakeup (Sleep Lock) : *효율적*

   - Semaphore 정의

     ```c
     typedef struct {
       int value;					/*semaphore*/
       struct process *L;	/*process wait queue*/
     } semaphore;
     ```

   - Block과 Wait

     - Block : 커널은 Block을 호출한 프로세스를 Suspend, 이 프로세스의 PCB를 Semaphore에 대한 Wait Queue에 삽입
     - Wakeup (P) : Block된 프로세스 P를 Wakeup, 이 프로세스의 PCB를 Ready Queue로 옮김

   - P(S) :

     ```c
     S.value--;
     if (S.value < 0) {
       add this process to S.L;
       block();
     }
     ```

     

   - V(S) : 자원이 반납되었음에도 0 이하라는 뜻은 다른 프로세스 Q가 자원을 사용했고 자원 수 S가 0 미만이 되어 Q가 Block되었다는 의미이므로 이미 Block되어 있던 프로세스 P를 깨움

     ```c
     S.value++;
     if (S.value <= 0) {
       remove a process P from S.L;
       wakeup(P);
     }
     ```

     *cf) S.value가 음수 : 어떤 프로세스가 자원을 기다리고 있음*

      	*S.value가 양수 : 자원의 여부가 있음 즉, 기다리지 않고 사용하는 상황*

> 일반적으로 Block/Wakeup 방법이 좋으나 Critical Section 길이가 매우 짧은 경우 Block/Wakeup방법이 오버헤드가 더 클 수 있음



### Two Types of Semaphores

1. Counting Semaphore

   : 도메인이 0 이상인 임의의 정수값

     주로 Resouce Counting에 사용

2. Binary Semaphore (= Mutex)

   : 0 또는 1

     주로 Mutual Exclusion (Lock / Unlock) 에 사용



### DeadLock and Starvation

**DeadLock** : 둘 이상의 프로세스가 서로 상대방에 의해 충족될 수 있는 Event를 무한히 기다리는 현상

Ex) S와 Q가 1로 초기화된 Semaphore라 하자

​			  P<sub>0</sub>	    	P<sub>1</sub>			P<sub>0</sub> 프로세스가 P(S)를 수행한 직후 CPU가 P<sub>1</sub> 프로세스로 넘어간다면?

​			P(S);		P(Q);

​			P(Q);		P(S);

​			  ...	 		...

​			V(S);		V(Q);

​			V(Q);		V(S);		  P<sub>0</sub> 프로세스와 P<sub>1</sub> 프로세스의 순서를 맞춘다면 (둘 다 P(S)를 실행하고 P(Q)를 실행한다면) 해결

**Starvation** : 프로세스가 Suspend된 이유에 해당하는 Semaphore 큐에서 빠져나갈 수 없는 현상 (Indefinite Blocking)

​						보통 몇몇 프로세스가 CPU를 독점하여 소수의 프로세스가 영원히 진전되지 않는 상태를 의미



### Dining-Philosophers Problem (식사하는 철학자 문제)

```c
do {
  P(chopstick[i]);
  P(chopstick[(i + 1) % 5]);
  ...
  eat();
  V(chopstick[i]);
  V(chopstick[(i + 1) % 5]);
  ...
  think();
  ...
} while (1);
```

![6-3-1](CS.assets/6-3-1.png)