# java기본1

데이터를 처리하는데 유리한 언어 - 자바

-> 전자 정부 프레임워크는 스프링 프레임워크(시스템을 구축할 때 중복되는 밑바탕) 기반이 많음

- OS(운영체제) : 시스템 하드웨어를 관리할 뿐 아니라 응용 소프트웨어를 실행하기 위하여 하드웨어 추상화 플랫폼과 공통 시스템 서비스를 제공하는 시스템 소프트웨어
- 프로그램 : 컴퓨터에서 실행될 때 특정 작업을 수행하는 일련의 명령어(약속된 단어)들의 집합
- JDK : JAVA 원시 프로그램을 컴파일
- JVM : 자바 바이트코드를 실행할 수 있는 주체
- 자바 바이트코드는 프랫폼에 독립적, 모든 자바 가상 머신은 자바 가상 머신 규격에 정의된대로 자바 바이트코드를 실행

# java기본2

### 컴퓨터의 자료표현

- 비트
- 바이트 : 8비트
- 2진수 
- 자바 메인 메소드 : 

# 변수와 타입1

```java
package live01;

public class Test {
    public static void main(String[] args) {
        System.out.print("Hello World\n");
        // \n 줄바꿈
        System.out.println("Hello World");
        System.out.println("\\"); // \
        System.out.println("\""); // "
        System.out.println("'"); // '
        // 주석은 작업지침에서 열외입니다.
        // ctrl shift f 정렬
        System.out.printf("%d \n", 10); //정수 (10진수)
        System.out.printf("%o \n", 10); //정수 (8진수)
        System.out.printf("%x \n", 10); //정수 (16진수)
		
        System.out.printf("%4d \n", 10); //4칸 확보후 오른쪽부터 차지            10
        System.out.printf("%-4d \n", 10); //4칸 확보후 왼쪽부터 차지           10
        System.out.printf("%04d \n", 10); //4칸 확보후 오른쪽부터 차지 빈공간 0  0010
        
        System.out.printf("%f \n", 10.1); //실수
        System.out.printf("%.2f \n", 10.1); //실수 (소수점 둘째자리까지)
        
        System.out.printf("%s \n", "오하민"); //문자열
        System.out.printf("%s의 나이는 %d입니다. \n", "오하민", "10");
        
        
        int a:
        a = 10;
        System.out.println(a);
        int b = 20;
        System.out.println(b);
		int c = a;
        System.out.println(c);

    }
}
// 실행은 ctrl f11
```

### 변수

- 데이터를 저장할 메모리의 위치를 나타내는 이흠
- 메모리상에 데이터를 보관할 수 있는 공간을 확보
- 적절한 메모리 공간을 확보하기 위해서 변수의 타입 등장
- '='을 통해서 CPU에게 연산작업을 의뢰

# 변수와타입2

```java
public class Test02 {
    public static void main(String[] args){
        short sa = 32767;
        //작은데 -> 큰데는 문제x (묵시적)
        int c = sa;
        //큰데 -> 작은데는 컨펌이 필요 (명시적)
        short sb = (short) c;
        
        float f = 10;
        //같은 크기라도 컨펌이 필요 (명시적)
        int g = (int) f;
    }
}
```

# 연산자

```java
public class Test03 {
    public static void main(String[] args){
        //사용자로부터 데이터 입력
        //자동완성으로 해야 자동 import
        Scanner sc = new Scanner(System.in);
        
        String name = sc.next();
        int age = sc.nextInt();
        int height = sc.nextInt();
        int weight = sc.nextInt();
        //연산
        //내림연산
        age = age / 10 * 10;
//      age = age - (age % 10);
        
        //반올림
        height = (height + 5) / 10 * 10;
    }
}
```

### 증감연산자

```java
int a = 5;
System.out.println(a++); //5
System.out.println(++a); //7
System.out.println(--a); //6
System.out.println(a);   //6
System.out.println(a--); //6
System.out.println(a++); //5
System.out.println(a);   //6
```

### 비교연산자

```java
int a = 10;

boolean b1 = a > 10;  // false
boolean b1 = a != 10; // false
boolean b1 = a >= 10; // true
```

### 삼항연산자

```java
//(true or false) ? 값1(true) : 값2(false)
```

### 조건연산자

```java
//피연산자, 결과 모두 boolean
&& 둘 다 참일경우 참
|| 둘 중 하나만 참이어도 참
! 반대로
```

### 배정연산자

```java
+=, -=, *=, /=
```

# 제어문

```java
public class Test04 {
    public static void main(String[] args){
		int n = 5;
        //if문
        //조건문에 문장을 두개 이상 묶으려면 중괄호 사용
        if ( n < 10 ) {
            System.out.println("이 문장을 수행");
            System.out.println("이 문장을 수행 too");
        }
        
        if ( n < 10 )
            System.out.println("이 문장을 수행");
        else
            System.out.println("이 문장을 수행함");
        
        int num;
        //값이 할당되어있지 않을 때 if 혼자 단독으로는 사용 불가
        if ( n < 10 )
            num = 10
        //else가 있어야 가능(실행 안 될 가능성이 없음)
        else
            num = 20
        System.out.println(num);
        
        if ( n > 90 )
            System.out.println("A");
        else if ( n > 80 )
            System.out.println("B");
        else
            System.out.println("F");
        
        //switch문
        int month = 12;
        switch(month) {
            case 1:
            case 3:
            case 5:
            case 7:
            case 8:
            case 10:
            case 12:
                System.out.println("31일");
                break;
            case 1:
            case 3:
            case 5:
            case 7:
                System.out.println("30일");
                break;
            case 2:
                System.out.println("아마 28일?");
            	break;
            default:
                System.out.println("제대로 입력하세요");
        }
    }
}
```

# 반복문

```java
public class Test05 {
    public static void main(String[] args){
        //if문과 기본적으로 같음 참이 아니면 그냥 지나감
        //하지만 거짓이 될때까지 반복
        int n = 5;
		while( n < 10 )
            System.out.println("이거 실행 됨??????"); //영원히 실행
        
        
        //조건문에 있는 값을 조작해야 함
        int n = 5;
		while( n < 10 )
            System.out.println("이거 실행 됨??????"); //5번 출력되고 n==10
        	n++;
        //헷갈리면 내가 데이터가 되어 한줄씩 실행한다.
        
        
        //만들다 보니 비슷하게 생김(변수초기화, 조건식, 내용, 변수의변화)
        //그래서 만들었다
        for(int i = 0; i < 5; i++){       //for(초기화; 조건; 변화){
            System.out.println("헤헤헿");  //    반복내용}
        }
            
        //do-while문은 조건을 나중에 평가하기 때문에 블록이 한번은 실행
        Scanner sc = new Scanner(System.in);
        int num = 0;
        do {
            System.out.print("숫자 : "); //숫자 : 입력값
            num = sc.nextInt();
        }while( num != 0 );             //처음값은 0이었지만 입력값으로 바뀌기때문에
        System.out.println("끝");       //0이 입력되면 종료
        //조건식에서 사용하는 변수가 반복 내용 안에서 결정이 될 때 사용(while에서도 가능)
            
        //whlie문으로 바꾼다면
        int num = 1;
        while( num != 0 ){
            System.out.print("숫자 : ");
            num = sc.nextInt();
        }
        
            
        for(int i = 0; i < 10; i++){
            System.out.println("헤헤");
            if ( i == 7 )
                break; //반복문 종료
        }
        
        for(int i = 0; i < 10; i++){
            if ( i == 7 )
                continue; //밑에 구문 건너뛰고 다음 루프로 이동
            System.out.println(i); // 7일때만 출력이 안됨
        }
    }
}
```

