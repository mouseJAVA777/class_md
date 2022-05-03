# 자바 문법2

#### 1. 1차원 배열

- 클라우드: 인프라를 빌려쓰는 것
- 드랍박스를 통해 공유할 예정
- 배열: 같은 타입의 변수의 모임

- String은 기초 자료형이 아니다(크기가 정해져 있지않음)
- int -> 정수하나 담을 수 있음
- int[] -> int 배열의 주소를 담을 수 있음(int랑 다른 타입임)
- new int[78]; -> int 78개 만큼의 공간을 만들어냄
- 
- ![image-20220430142947977](java_2.assets/image-20220430142947977.png)

- 장점:  1. 간편하게 많은 같은 타입의 변수를 생성할 수 있다.
  2. 연속된 공간을 할당 받을 수 있다.
  3. 반복문과의 시너지
- 배열이란
  - 같은 종류의 데이터를 저장하기 위한 자료구조
  - 크기가 고정되어 있다.(한번 생성된 배열은 크기를 바꿀 수 없다.)
  - 배열을 객체로 취급
  - 배열의 요소를 참조하려면 배열이름과 색인이라고 하는 
    int 유형의 정수값을 조합하여 사용한다.
  - ![image-20220430153629503](java_2.assets/image-20220430153629503.png)

```java
public class test01 {
    public static void main(String[] args) {
        Scanner sc = new Scanner (System.in);
        System.out.println("몇번을 보고 싶어요?");
        int num = sc.nextInt();
        int[] score = new int[78];
        score[0] = 10;
        score[1] = 12;

        System.out.println(score[num]);

        int score0 = 10;
        int score1 = 12;
    }
}
```

```java
public class test02 {
    public static void main(String[] args) {
        int[] score = new int[5];
        score[0] = 10;
        score[1] = 12;
        score[2] = 17;
        score[3] = 20;
        score[4] = 1;

        for (int i = 0; i < 5; i++) {
            System.out.println(score[i]);
        }

        // score에 들어있는 데이터 중 가장 큰 데이터를 찾자.
        // 젤 큰 녀석을 찾고
        // 그 녀석과 0번칸의 위치를 교환
        int max = score[0];
        int maxIdx = 0;
        for (int i = 0; i < score.length; i++) {
            if (max < score[i]) {
                max = score[i];
                maxIdx = i;
            }
        }
        System.out.println(max);
        System.out.println(maxIdx);

        int tmp = score[0];
        score[0] = score[maxIdx];
        score[maxIdx] = tmp;
        System.out.println(score[0]);
    }
}
```

```java
public class test03 {
    public static void main(String[] args) {
        int a = 10;
        int b = 20;

        // doSomething
        int tmp = a;
        a= b;
        b= tmp;

        System.out.printf("%d %d", a, b);
    }
}
```

```java
import java.util.Arrays;

public class test04 {
    public static void main(String[] args) {
        int[] score = new int[5];
        score[0] = 10;
        score[1] = 12;
        score[2] = 17;
        score[3] = 20;
        score[4] = 1;

        // for-each
        // score에 값을 n에 복사해서 쓰는거임.
        for (int n : score) {
            System.out.println(n);
        }

        int a = 10;
        int b = a;
        a = 12;
        System.out.println(b);

        System.out.println(Arrays.toString(score)); // 예쁘게 나옴
        // output : [10, 12, 17, 20, 1]
    }
}
```

- ![image-20220430154154616](java_2.assets/image-20220430154154616.png)
- 스트링 배열타입(String[]) - 스트링이 여러개 담긴 위치를 담은 배열의 위치를 참조할 수 있는
  공간을 만듬
- ex) String name = 'hong'; -> 문자열 하나의 위치를 저장할 수 있는 공간
- String nameList = new String[3]; -> 문자열 하나의 위치를 저장할 수 있는 공간이 여러개
  모여있는 아이를 참조할 수 있는 공간
- int a = 10; / 정수를 하나 저장할 수 있는 공간
- int[] arr = new int[10];  / **int[10]** -> 정수 10개가 모여 있는 공간
  **int[]** -> 정수가 10개 모여 있는 **공간의 위치**를 저장할 수 있는 공간
  `int[][]` -> int[]가 또 여러개 있는거

- ![image-20220430155228780](java_2.assets/image-20220430155228780.png)
- ![image-20220430155242640](java_2.assets/image-20220430155242640.png)
- `prime = new int[3][];` --> 참조까지만 하고 있고, 2차원 뎁스에 있는녀석들은
  아직 만들지 않았음

#### 1-2. 배열의 자동 초기화

- 배열이 생성되면 자동적으로 배열요소는 기본값으로 초기화된다.

- int: 0
- boolean : false
- char : `\u0000'
- 참조형 : null...,
- 멤버변수와 로컬변수 모두 배열이 생성이 되면 자동 초기화된다.
- ![image-20220430155638333](java_2.assets/image-20220430155638333.png)
- ![image-20220430155647368](java_2.assets/image-20220430155647368.png)
- ![image-20220430155727538](java_2.assets/image-20220430155727538.png)
- 초기화
  - {} 를 활용하는 방식: 배열 선언 시 에만 설정가능
  - 1차원 배열: 배열유형 [] 배열명 = {값, ..값};
  - ex) int [] prime = {1, 2, 3};
  - 2차원 배열: 배열유형 `[][]` 배열명 = {{ 값1, 값2}, {값3, 값4}};
  - ex) int `[][]` twoArr = {{1, 2}, {3, 4}, {5, 6}};
  - new 배열타입[] {값, ...,}
  - int [] prime = new int[] {1, 2};

#### 1-3. 배열 관련 제공 API

- ![image-20220430160131326](java_2.assets/image-20220430160131326.png)

#### 1-4. 배열의 메모리 생성 과정

- ![image-20220430160225020](java_2.assets/image-20220430160225020.png)

#### 1-5. for-each

- 가독성이 개선된 반복문으로, 배열 및 collections에서 사용
- index 대신 직접 요소(elements)에 접근하는 변수를 제공
- naturally read only (copied value)
- ![image-20220430160341025](java_2.assets/image-20220430160341025.png)
- 