# 상속(Inheritance)

### 상속

다른 클래스가 가지고 있는 변수나 함수를마치 내꺼처럼 물려받는거



### Super class - 부모가 되는거

### Sub class - 자식이 되는거



```java
public class Person{
    String name;
    int age;
    
    public void eat() {
        System.out.println("음식을 먹는다.");
    }
}
```

```java
public class Student {
    String name;  
    int age;  
    String major;
    
    public void eat() {
        System.out.println("음식을 먹는다.");
    }
    public void study() {
        System.out.println("공부를 한다.")
    }
}
```



```java
String name;  
int age;

public void eat() {
    System.out.println("음식을 먹는다.");
}

// 요 부분이 겹친다.
// 코드 낭비 & 복잡도를 올린다.
//
```
상속을 받으면
```java
public class Student extends Person {
    String major;
    
    public void study() {
        System.out.println("공부를 한다.")
    }
}
// extends 옆의 class를 상속받는다.
//부모가 가지고 있는 변수와 함수도 자식안에 같이 존재한다.
```



# Object

```java
public class Student // 여기에는 extends Object가 생략되어 있는거다
```

모든 자바상의 클래스들은 object 타입의 멤버들을 가지고 있다.



- 가장 최상위 클래스로 모든 클래스의 조상
- Object의 멤버는 모든 클래스의 멤버

![image-20220602141410701](상속(Inheritance).assets/image-20220602141410701.png)

### 정리

1. 확장성, 재 사용성
   1. 부모의 생성자와 초기화 블록은 상속 x
2. 클래스 선언시 extends 키워드를 명시
3. 관계
   - 부모(상위, Super)클래스 : Person
   - 자식(하위, Sub)클래스 : Student
4. 자식 클래스는 부모 클래스의 멤버변수, 메소드를 자신의 것처럼 사용할 수 있다( 단, 접근 제한자에 따라 사용 여부가 달라진다.)
5. Object 클래스는 모든 클래스의 조상 클래스
   - 별도의 extends 선언이 없는 클래스는 extends Object가 생략



### 상속의 동작 원리를 알아보자

```java

class Parent {
    int data = 10;
    Parent(){
        System.out.println("Parent 클래스의 생성자");
    }
    //기본생성자가 아닐경우
    //Parent(int data){
    	//this.data = data;
		//System.out.println("Parent 클래스의 생성자");
	//}
}
class Child extends Parent{
    String name;
    Child(){
        super(); //부모 클래스 생성자의 호출, 상속을 받으면 생성자의 첫 줄에서 이 문장을 수행하게 됨
		//super(); 암묵적으로 부모클래스의 생성자를 가져오는게 적혀있다
        //super(10); 부모클래스의 생성자 조건에 맞는 생성자 호출
        System.out.println("Child 클래스의 생성자");
    }
}
public class ExtendsTest {
    public static void main(String[] args){
        Child c = new Child();
    }
}
	
//결과
//"Parent 클래스의 생성자"
//"Child 클래스의 생성자"

// 자식 클래스의 객체를 생성하는 것은,
// 부모 클래스의 객체를 먼저 선언한 후,
// 거기에 자식 클래스를 이어 붙여서 객체생성을 완성
```



### 부모클래스의 변수명과 자식클래스의 변수명과 같을 수 있냐???



```java
class Person{
    String name;
    int age;
    
    public void eat() {
        System.out.println("음식을 먹는다.");
    }
}
class Student extends Person {                 // Person클래스를 상속받음
    String major;
    
    public void study() {
        System.out.println("공부를 한다.")
    }
    public void eat(){                                          
        super.eat(); //부모의 eat() 실행 즉 "음식을 먹는다."
        System.out.println("급식을 먹는다.")
    }
}
public class PersonTest {
    public static void main(String[] args) {
        Student s = new Student();
        s.study(); // "공부를 한다."
        s.eat(); // "급식을 먹는다."
    }
}
```

// eat함수를 자식클래스에서 조금 더 확장시켜서 사용하고 싶다???



### 오버라이딩(overriding)

- 상위 클래스에 선언된 메서드를 자식 클래스에서 재정의 하는 것
- 메서드의 이름, 반환명, 매개변수 (타입, 개수, 순서) 동일 해야한다.
- 하위 클래스의 접근제어자 범위가 상위 클래스보다 크거나 같아야 한다.
- 반환유형이 같아야하고 함수명 같아야함 매개변수의 개수도 타입도 순서도 전부 다 같아야한다.

- 부모가 public인데 자식이 private로 작아질 수 없다.



### super

- 부모의 멤버에 접근하기 위해서 super 키워드 사용





```java

class Parent {
    int data = 10;
    public void print() {
        System.out.println(data);
    }
}
class Child extends Parent{
    int data = 20;
    public void print() {
        int data = 30;
        System.out.println(data);                // 30
        System.out.println(this.data);           // 20
        System.out.println(super.data);          // 10
}
public class ExtendsTest {
    public static void main(String[] args){
        Child c = new Child();
        c.print();
    }
}

```



# 상속과 다형성 복습

### ![image-20220602155651978](상속(Inheritance).assets/image-20220602155651978.png)

부모가 먼저 만들어지고 거기에 Student가 붙어서 만들어진다.



### 다형성

- 다형성이란 많은 형상을 가질 수 잇는 성질
- 부모클래스의 참조변수가 자식클래스의 객체를 참조할 수 있다. 왜?? 당연하지 부모를 먼저 만들고 자식을 이어붙였으니까
- 부모클래스가 자식클래스의 객체를 참조할 수 있지만 실제 부모영역만 접근이 가능하다 -------------------> 무슨말이냐???
- Person p = new Student("박싸피", 20, "수학");  요기서 new Student에서 만든애를 Object 클래스의 참조변수인 o에 참조 가능한가?? 가능은 한데 o.name을 찍어보면 없다  Object만 쳐다보기 때문에 name 같은거에는 접근 불가능
- p로 접근하면은 p.equals() 가능한가? 가능하다!!! why?? Object 만들고 Person 만들고 Student 만드니까 object에 있다

![image-20220602160805282](상속(Inheritance).assets/image-20220602160805282.png)



![image-20220602162428353](상속(Inheritance).assets/image-20220602162428353.png)

부모 클래스의 참조 변수로 자식객체를 참조하고 있으면 부모 영역만 접근 가능하니까 자식까지 접근하고 싶으면 형 변환을 하면 된다. 

형변환을 잘못하면 class test exception(?) 가 발생할 수 있다. 그러므로 형변환 하기 전에 instance of 키워드를 사용하자. 

![image-20220602162610540](상속(Inheritance).assets/image-20220602162610540.png)

person 변수가 현재 참조하고 있는 실제 객체가 Student 타입으로 참조가 가능한지 연산하는 연산자이다 위에 예제는 false이다.



### 동적 바인딩

- 함수가 오버라이딩 되어 있으면 자식의 메소드가 호출된다.

![image-20220602163446817](상속(Inheritance).assets/image-20220602163446817.png)
