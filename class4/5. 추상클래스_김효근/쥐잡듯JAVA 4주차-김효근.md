# 쥐잡듯JAVA 4주차

## 추상클래스 복습

### 추상 클래스의 사용 기원

1. 동적 바인딩 사용하기 위해
2. 형변환을 해서 사용하기에 귀찮음
3. 하위 클래스에서 반드시 오버라이딩해서 사용되는 함수가 있다면,
   일단 동적 바인딩을 위해 정의는 해주어야하는데 담을 내용은 없기 때문에
   추상클래스라는 것으로 만든다

### 추상 클래스 정의

> 객체를 생성할 수 없는 클래스라는 의미로 클래스 선언부에 abstract를 추가
>
> 메서드의 구현부는 ;(세미콜론)으로 대체
>
> 메서드의 선언부에도 abstract 키워드 추가

- 자손 클래스에서 `반드시` 재정의해서 사용되기 때문에 조상의 구현이 무의미
- 추상 클래스는 미완성이기 때문에, 객체로 만들 수 없다
- 타입으로서는 동작이 가능하다

```java
public abstract class Chef { //-> 추상메소드를 하나라도 가지고 있는 클래스는 추상클래스
    String name;
    int age;
    String speciality;
    
    public void eat() {
        System.out.println("음식을 먹는다.")
    }
    public abstract void cook(); //=> 미완성 함수 == 추상메소드
}
```

### 추상메소드 구현 의무

추상 클래스를 상속 받으면, 추상 메소드를 구현해야하는 __의무__가 존재한다

의무를 이행하지 않는다면, 추상클래스로 전염되어야한다.

### 익명 클래스

추상 클래스로 객체를 생성할 때, 미완성된 부분을 임시로 메꾸어 주어 사용 가능하다

1회용 구현

```java
Chef c2 = new Chef() {
    @Override
    public void cook() {
        System.out.println("추상메소드의 1회용 구현")
    }
}
```

### 추상클래스 특징

- abstract 클래스는 상속 전용의 클래스

- 클래스에 구현부가 없는 메서드가 있으므로 객체를 생성할 수 없음

- 상위 클래스 타입으로 자식을 참조할 수는 있음

  ```java
  //생성할 수 없음
  Chef chef1 = new Chef();
  //참조는 문제 없음
  Chef chef2 = new KFoodChef();
  ```

- 조상 클래스에서 상속받은 abstract 메서드를 재정의 하지 않는 경우
  자식 클래스 또한 abstract 클래스가 되던가, 구현하던가 둘 중 하나를 골라야 함

### 추상 클래스 사용하는 이유

- abstract 클래스는 구현의 강제를 통해 프로그램의 안정성 향상



### 인터페이스

> 추상메소드의 모임

- 완벽한 추상화된 객체 : 모든 메서드가 abstract 형태
- 반쯤 완성된 객체
- 설계도

```java
public interface MyInterface {
    public static final int MEMBER1 = 10;
    int MEMBER2 = 10;
    public abstract void method1(int param);
    void method2(int param);
}
```

1. interface 키워드를 이용하여 선언

2. 선언되는 변수는 모두 상수로 적용됨

   - 위의 MEMBER2도 상수

3. 선언되는 메소드는 모두 추상 메소드로 적용됨

   - 위의 method2도 추상메소드

4. 객체 생성이 불가능하지만 타입으로는 작동함

5. 클래스가 인터페이스를 상속할 경우에는 extends 키워드가 아니라 implements 키워드를 사용

   ```java
   interface Shape {}
   class Circle implements Shape {}
   //여러개의 interface implements 가능
   ```

6. 인터페이스를 상속받는 하위 클래스는 추상 메소드를 반드시 오버라이딩 해야 한다.
   구현하지 않을 경우 abstract 클래스로 표시

   ```java
   interface Chef{
       void cook();
   }
   class KFoodChef implements Chef {
       @Override
       public void cook() {
           System.out.println("한식을 요리한다")
       }
   }
   ```

7. 인터페이스 다형성 적용

### 인터페이스의 필요성

- 구현의 강제로 표준화 처리
- 인터페이스를 통한 간접적인 클래스 사용으로 손쉬운 모듈 교체 지원
- 서로 상속의 관계가 없는 클래스들에게 인터페이스를 통한 관계 부여로 다형성 확장
- 모듈 간 독립적 프로그래밍 가능 -> 개발 기간 단축





```java
//StudentManager - 기능
public class StudentManager implements IStudentManager {
	private static final int MAX = 100;
    private Student[] students = new Student[MAX];
    private int size = 0;
    @Override
    public void add(Student s) {        
        sutdents[size++] = s;
    }
    @Override
    public Student[] getStudentList() {
        return null;
    }
	@Override
    public Student getStudentByName(String name) {
        return null;
    }
    @Override
    public void changeMajor(String name, String major) {
        
    }
}
```

```java
//Interface
public interface IStudentManager {
    void add(Student s);
    Student[] getStudentList();
    Student getStudentByName(String name);
    void changeMajor(String name, String major);
}
```

```java
//StudentUI - UI
import java.util.Scanner;
public class StudentUI {
    //private IStudentManager sm;
    //private IStudentManager sm = new StudentManager();
    private IStudentManager sm = new StudentManagerV2(); //모듈 교체
    public void run() {
        Scanner sc = new Scanner(System.in);
        int sel;
        do{
            System.out.println("1. 학생추가");
            sel = sc.nextInt();
            if(sel == 1) {
                String name = sc.next();
                int age = sc.nextInt();
                String major = sc.next();
                Student s = new Student();
                s.setName(name);
                s.setAge(age);
                s.setMajor(major);
                sm.add(s);
            }
        }while(sel!=0);
    }
}
```

