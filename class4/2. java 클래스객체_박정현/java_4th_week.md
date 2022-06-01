## 클래스/객체/상속/접근제한자

학생관리 프로그램

- 이 부분을 공부하고 나서 ...
  - class 생성을 올바르게 할 수 있다 (자료형, 함수 상관없이 뭐든 가능)
  - class를 이용해 객체를 올바르게 생성할 수 있다
  - 생성한 객체를 조회할 수 있다
  - 생성한 객체의 값을 적절히 변경할 수 있다
  - 클래스 내에 선언된 함수를 활용할 수 있다

1. main

```java
package 학생관리;

import java.util.Scanner;

public class StudentTest {
	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		StudentManager sm = new StudentManager();
		int sel;
		do {
			System.out.println("번호로 입력하세요");
			System.out.println("1. 학생추가 ");
			System.out.println("2. 학생조회(이름) ");
			System.out.println("3. 전공변경 ");
			System.out.println("0. 종료 ");
			sel = sc.nextInt();
			if (sel == 1) {
				System.out.println("학생을 추가합니다.");
				System.out.println("이름: ");
				String name = sc.next();
				System.out.println("나이: ");
				int age = sc.nextInt();
				System.out.println("전공: ");
				String major = sc.next();
				Student s = new Student(); // 객체 생성하고
				s.name = name; // 객체에 값을 담아주자
				s.age = age;
				s.major = major;
//				students[size++] = s; // 값을 담아놓은 s를 size 위치에 담고, size의 값을 1 증가시키자
				sm.addStudent(s);
			} else if (sel == 2) {
				System.out.println("학생을 조회합니다.");
				System.out.print("이름: ");
				String name = sc.next();
				Student s = sm.getStudent(name);
				if (s == null) {
					System.out.println("해당하는 학생이 존재하지 않습니다.");
				} else {
					System.out.println("조회한 학생의 정보는 ");
					System.out.println("이름: " + s.name);
					System.out.println("나이: " + s.age);
					System.out.println("전공: " + s.major);
				}
			} else if (sel == 3) {
				System.out.println("전공을 변경합니다.");
				System.out.print("이름: ");
				String name = sc.next();
				System.out.print("전공: ");
				String major = sc.next();
				sm.changeMajor(name, major);
				
			}
			
		} while(sel != 0);
		
		sc.close();
	}
}

```

2. 함수 part

```java
package 학생관리;

public class StudentManager {
	Student[] students = new Student[100];
	int size = 0;
	
	void addStudent(Student s) {
		students[size++] = s;
	}
	
	void changeMajor(String name, String major) {
		Student s = getStudent(name);
		if (s == null) {
			
		} else {
			s.major = major;
		}
	}
	Student getStudent(String name) {
		int idx = -1;
		for (int i = 0; i < size; i++) {
			if (name.equals(students[i].name)) {
				idx = i;
				break;
			}
		}
		if (idx == -1) {
			return null;
		} else {
			return students[idx];
		}
	}
}

```



## 이클립스 보면서 설명