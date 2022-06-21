## 클래스, 생성자

---

## 클래스



**이해를 돕기 위한 표현**

배열이 같은 타입의 데이터의 모임이라면? **클래스는 다른 타입의 데이터(물론 반드시 다를 필요는 없음. 다를수도 있는 데이터 정도라고 생각하면 될듯)들의 모임**이라고 **일단** 생각해두자

```java
public class PersonTest {
    public static void main(Stirng[] args) {
        String name1 = "Park";
        String name2 = "Hong";
        
        int age1 = 18;
        int age2 = 30;
        
        int height1 = 198;
        int height2 = 180;
        // 배열의 경우 같은 타입의 친구들(위의 코드를 예로 들자면 Park-Hong, 18-30, 198-180)끼리 요소로 넣어주었다
        // 그럼 클래스는? 사용자가 어떠한 공간을 만든다고 생각하면 됨
        // 그 공간엔 여러 타입의 변수들이 들어있을 수 있음
    }
}
```

int로 선언된 공간엔 int타입의 값이 들어감

String으로 선언된 공간엔 문자열의 위치 정보가 들어감

class로 선언된 공간엔 사용자가 원하는 타입들의 정보 및 값이 묶음으로 들어감

**class 만들기**

```java
public class Person { // class라는 키워드에 적당한 이름을 지어주고
    String name; // 그 안에 사용할 것들을 넣어주자
    int age; // 이렇게 다양한 타입을
    int height; // 사용자가 원하는대로 넣을 수 있다
}
```



위에서 만들어 준 Person 클래스를 생각해보자

해당 클래스는 길이가 정해져있는가? 아니다. 그러면?

**실제 데이터는 길이가 정해지지 않은 정보를 넣을 수 있는 공간**에 집어넣고, **그 공간의 위치를 기억**하는 방식

```java
Person p1 = new Person(); // class를 이용해 찍어낸 데이터
p1.name = "Park"; // 해당 클래스로 찍어낸 p는 .을 이용해 정해둔 요소들에 접근 가능
p1.age = "18";
p1.height = "198";

Person p2 = new Person();
p2.name = "Hong";
p2.age = "30";
p2.height = "180";
```

class는 묶음도장... String name; int age; int height; 등은 그냥 도장 (라이브에 나온 비유인데 와닿아서 써둠)

---

갑자기 **함수**

자주 쓰일 것 같은 명령어를 **재사용할 목적**으로 이름 붙여둔 것

+

매개변수를 넣어 뚜쉬뚜쉬뚜쉬

+

return 뚜쉬뚜쉬 (지금은 추상적으로만)

```java
public class FunctionTest {
    public static void main(String[] args) { // return값 없을 때 void 씀. 그 외의 경우 return의 타입을 써줌
        work("자동차");
        work("자전거");
    }
    static void work(String name) {
        System.out.println(name + "를 타고 출퇴근한다");
    }
}
```

---

다시 **클래스**

위에서 본 함수를 적용해보자

```java
static void printPerson(Person p) { // 원래 함수 만들때 안에 매개변수의 타입이랑 매개변수 넣어줬었음
    // 그럼 p의 타입은? -> Person 타입
    System.out.println("사람의 이름은 " + p.name)
}
```

```java
printPerson(p1); // "사람의 이름은 Park"
printPerson(p2); // "사람의 이름은 Hong"
```

클래스 안에 함수넣기 가능? **가능**

위에서 썼던 Person class를 가져와보자

```java
public class Person {
    String name;
    int age;
    int height;
    
    void print(){ // 힘수 넣기 가능
        System.out.println("사람의 이름은 " + name); // p.name이 아닌 name. 같은 클래스에 name이 지정되어있기 때문
    }
}
```

```java
p1.print(); // "사람의 이름은 Park" -> p1의 print 실행 -> print 속의 name 변수는 p1의 name
p2.print(); // "사람의 이름은 Hong"
```

**여기까지 본 시점에서, class에 대한 정의를 다시 해보자**

변수, 함수를 묶어 만들어낸 **사용자 정의 자료형** (위에 printPerson 함수 만들어 줄 때 Person p 라고 넣어줬던걸 잊지 말자)

---

--개론적인 내용--

**객체**

객체는 클래스로부터 만들어진다

**클래스는 객체를 생성하는 틀임**. 생성된 **객체**는 어떠한 특징**(속성 및 동작)**을 지님

속성? -> 멤버 변수, 동작? -> 메소드



**추상화와 클래스**

필요한 객체를 설계하여 프로그램이 인식하게 하는 방법임

---

## 생성자



생성자란? 객체가 실행될 때 최초 한번 실행되는 함수를 의미한다

생성자는 클래스와 함수명이 같음

**생성자를 만들지 않으면? 몸통이 비어있는 기본 생성자를 컴파일러가 자동으로 생성해 줌**

```java
Person p1 = new Person(); // Person()이 생성자임
```

```java
public class Person {
    String name;
    int age;
    int height;
    
    Person(){ // 이런 기본 생성자를 자동으로 생성해 줌. 위의 Person()은 이걸 호출한 것
        
    }
    
    void print(){ // 힘수 넣기 가능
        System.out.println("사람의 이름은 " + name);
    }
}
```

생성자도 함수니까, **필요하다면 매개변수를 받을 수 있다**

즉, `Person(String n, int a, int h) { name = n; age = a; height = h; }`와 같은 식으로 생성자를 만들어 두면

호출시 매개변수를 집어넣어주는 방식으로 좀 더 편하게 객체와 속성 정의 가능

```java
Person p1 = new Person("Park", 18, 198); // -> 하나씩 집어넣는것보다 편리함
```



**생성자의 특징**

1. **클래스명과 이름이 동일**

2. **반환타입이 없다**

3. **디폴트 생성자(기본 생성자)**

4. **오버로딩 지원**(똑같은 이름의 생성자라 할지라도, 매개변수의 개수 및 타입 등에 따라 서로 다른 생성자를 만들 수 있음)

5. 객체를 생성할 때 **속성의 초기화**를 담당

6. **this** 가 왜 여기서 나오지

   ```java
   public class Person {
       String name;
       int age;
       int height;
       
       Person(String n, int a, int h) {
           name = n;
           age = a;
           height = h;
       }
       
       void print() {
           int age = 10;
           System.out.println("사람의 이름은 " + this.age + "입니다.");
       }
   }
   ```

   ```java
   Person p = new Person("park", 18, 198); // 객체 생성
   p.print(); // 어떻게 동작하나?
   // 1. 10살이다
   // 2. 18살이다
   // this.age 이므로 18살이 맞음
   // 그냥 age 였으면 10살
   // 어떻게 동작하는가?
   // 일단 해당 클래스 안에 2개의 age가 있다. class에 정의된 age와 메소드에 정의된 age
   // age를 쓸 경우, 기본적으로 가장 가까운 위치의 변수를 찾아간다
   // print 메소드의 경우 해당 println문의 age와 가까운 변수가 print메소드 안의 age이므로 10살이 됨
   // 근데 거기서 age 앞에 this를 붙여주게 되면?
   // this를 쓰는 순간 해당 위치를 class로 옮겨가게 됨
   // class에서 바라볼 때, 가장 가까운 age변수는? class에 정의된 age, 즉 생성자 호출시 넣어준 18세가 보여지게 됨
   ```

   +

   this의 두번째 역할: 다른 생성자를 호출할 때 이용됨

   ```java
   ...
       Person(String name, int age, int height) {
       	this.name = name;
       	this.age = age;
       	this.height = height;
   	}
   	
   	Person() {
           this("Park", 18, 198);
           // 다른 생성자를 호출할때는 이름 대신 this 키워드를 쓰자
           // 다른 생성자를 호출하려면 현재 생성자에서 아직 아무것도 하지 않은 상태여야 함
           // 규칙
       }
   ...
   ```

   

