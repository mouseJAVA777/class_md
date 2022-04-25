# 쥐잡듯안JAVA 1주차 - 김효근

## 조건문

### IF문

```java
//자바
if (조건식) {
    System.out.println("~~");
}
else if (조건식) {
    System.out.println("?~");
}
else 
    System.out.println("!~")
```

중괄호(`{}`)를 사용하지 않으면 if문 바로 아래의 실행문장만 실행되기때문에

왠만하면 중괄호를 계속 붙여서 사용하는 것이 나을 것 같다.

```python
#파이썬
if 조건식 :
    print("~~")
elif :
    print("?~")
else :
    print("!~")
```



### SWITCH문

```java
switch(수식){
    case value1 :
        처리문장;
        break;
    case value2 :
        처리문장;
        break;
    case value3 :
        처리문장;
        break;
    default :
        묵시적으로 처리해야하는 문장들;
}
```

수식의 값이 case문에 알맞는 값이라면 해당 case문으로 이동하여 처리문장을 진행하고,

아래방향으로 코드를 읽어나간다. 다만 break가 없다면 해당 case문 아래로 모두 실행한다.

그러므로 하나의 케이스에 고정하려면 break가 반드시 입력되어야한다.

모든 case문에 적합하지 않다면 default문을 지정해서 기본값을 부여할 수 있다.

```java
//예시
switch(month){
    case 1:
    case 3:
    case 5:
    case 7:
    case 8:
    case 10:
    case 12:
        System.out.println("31일");
        break;
    case 4:
    case 6:
    case 9 :
    case 11:
        System.out.println("30일");
        break;
    case 2 :
        System.out.println("28인데, 윤년인지 확인해야되요")
        break;
    default :
        System.out.println("그런 월은 존재하지 않습니다")
}
```



