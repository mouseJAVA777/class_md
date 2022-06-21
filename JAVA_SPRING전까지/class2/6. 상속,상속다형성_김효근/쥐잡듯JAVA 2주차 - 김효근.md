# 쥐잡듯JAVA 2주차 - 김효근

## 상속

> __어떤 클래스의 특성을 그대로 갖는 새로운 클래스를 정의한 것__

### Super Class (상위 클래스, 부모 클래스)

- 사람 = name, age

### Sub Class (하위 클래스, 자식 클래스)

- 선생 = name, age, subject

- 개발자 = name, age, language
- 요리사 = name, age, foodtype

Sub Class 에는 공통된 요소들이 존재하고 이것을 하나로 묶어 Super Class가 가지고 있는 요소로 만든 다음, SuperClass를 상속받는 SubClass를 사용하면 요소를 매번 새로 지정해주지 않아도 원래 가지고 있는 요소로 사용할 수 있다.

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
    String name;  //겹침
    int age;  //겹침
    String major;
    //겹침
    public void eat() {
        System.out.println("음식을 먹는다.");
    }
    public void study() {
        System.out.println("공부를 한다.")
    }
}
```

#### 상속을 받는다면

```java
public class Student extends Person {
    String major;
    
    public void study() {
        System.out.println("공부를 한다.")
    }
}
```



### Object

##### 모든 클래스들은 extends Object를 기본값으로 가지고 있다.



### 객체의 생성

자식 클래스의 객체를 생성하는 것은

1. 부모클래스의 객체를 `먼저 선언한` 후,

2. 자식클래스를 이어 붙여서 객체 생성을 완성하는 것이다.

#### 주의사항

- 부모클래스의 기본생성자(생성자 정의가 없을때 컴파일러가 자동적으로 생성해주는 생성자)가 존재하지 않는다면, 자식 클래스 생성자의 첫 줄에서 명시적으로 부모클래스의 생성자를 호출해주어야함

```java
// Parent extends Object
class Parent {
    int data = 10;
    Parent(){
        System.out.println("Parent 클래스의 생성자");
    }
    //기본생성자가 아닐경우
    //Parent(int data){
    	//his.data = data;
		//System.out.println("Parent 클래스의 생성자");
	//}
}
class Child extends Parent{
    String name;
    Child(){
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
```



### 오버라이딩

부모가 정의한 변수나 함수를 자식이 똑같이 재정의 하는 것

- 반환 유형이 같아야함
- 함수 명이 같아야함
- 매개변수의 개수와 타입과 순서가 같아야함
- 접근제한이 부모보다 더 작아질 수 없다 (부모에서 public으로 정의된게 자식에서 private으로 정의 불가능)

```java
class Person{
    String name;
    int age;
    
    public void eat() {
        System.out.println("음식을 먹는다.");
    }
}
class Student extends Person {
    String major;
    
    public void study() {
        System.out.println("공부를 한다.")
    }
    @Override //오버라이드의 재확인
    public void eat(){
        super.eat(); //부모의 eat() 실행
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

### super 키워드

- super를 통해 조상클래스의 메소드 호출 가능



### Final

- 변수의 상수화 

  ```java
  final int a = 10;
  a = 20;
  //a는 10으로 고정됌
  ```

- 메소드의 오버라이딩 금지

  ```java
  class Printer{
      public final void print(){}
  }
  
  class SSPrinter extends Printer{
      //오류 발생
      public void print (){
          System.out.println("재정의")
      }
  }
  ```

- 클래스의 상속 금지

  ```java
  final class String {
      public void print (){}
  }
  //오류 발생
  class MyString extends String {
      public void print(){
          System.out.println("재정의")
      }
  }
  ```

  

### 접근 제한자

- private : 자신만 접근 가능
- default : 같은 패키지 내에서만 접근 가능
- protected : 같은 패키지 내에서만 접근 가능하거나, 다른 패키지에서 자손일 경우 접근 가능
- public : 누구나 어디서든 접근 가능

