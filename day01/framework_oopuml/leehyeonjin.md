# OOP(Object Oriented Programming)

---

### 절차 지향 개발의 문제점

- 여러 용도로 사용되는 함수들이 많아짐으로써, 소스코드 변경시 여러 곳에 영향을 끼쳐 유지보수가 어려움.
- 역할 분배하기가 애매해서 협업이 어려움.
- 전역변수를 마구 사용하다보면, 기능추가로 인한 부작용 발생가능성이 높음.

### 객체 지향 개발 장점

> OOP 방식은 **변경에 유연**하다.
>
- 큰 규모의 개발시, 독립적으로 수행하는 역할을 나누어 운영하는 시스템화가 필요하다.
- 외부에서 만든 객체를 가져다 사용하면 되므로, 재사용성이 좋음.
- 연관된 클래스만 코드를 변경하면 되므로, 유지보수성이 좋음.
- 담당 파트를 정하기 편리하므로, 협업하기가 더 나음.

---

### 클래스( Java )

![Untitled.png](..%2F..%2F..%2F..%2F..%2F..%2FDownloads%2FUntitled.png)
- 클래스( 전역변수 + 함수 = 하나의 타입 ) 중심의 개발 → 객체 단위로 개발이 가능해짐.

```java
public class Marin {
	int hp = 100;

	void run() {
		hp -= 10;
		System.out.println("RUN " + hp);
	}
}

public class Zergling {
	int hp = 80;
	int mana = 200;

	void attck() {
		hp += 1;
		mana -= 100;
	}

	void move() {
		hp -= 10;
		mana += 5;
	}

	void status() {
		System.out.println("STATUS : hp " + hp + " mana " + mana);
	}
}

public class Main {
	public static void main(String[] args) {
		// new를 통한 사용자 정의 타입(클래스) 초기화
		// java는 객체가 heap 영역에 저장되기 때문에 new 키워드를 통한 초기화 필요
		Marin marin1 = new Marin();
		System.out.println(marin1.hp);

		// Marin 템플릿을 통해 제작해낸 실체(인스턴스) 객체
		// 인스턴스를 통해서만 내부 속성, 동작에 접근가능
		marin1.run();
		marin1.run();
		marin1.run();
		marin1.run();
		marin1.run();

		// 사용이 완료된(더 이상 참조X) 객체는 GC에 의해 자동삭제

		Zergling zergling1 = new Zergling();
		zergling1.status();
		zergling1.attck();
		zergling1.move();
		zergling1.status();
		Zergling zergling2 = new Zergling();
		zergling2.status();
		zergling2.attck();
		zergling2.move();
		zergling2.status();
	}
}
```

---

### Server Code 와 Client Code

Server Code

- Client 요청을 받으면, 처리해주는 코드.
- Library == Server Code.

Client Code

- Server Code에게 일을 요청하는 코드.
- Library 사용자 == Client Code.

```java
class Calculator { // server code
	int result;

	void plus(int a, int b) {
		result = a + b;
	}

	void minus(int a, int b) {
		result = a - b;
	}

	void divide(int a, int b) {
		result = a / b;
	}

	void multiple(int a, int b) {
		result = a * b;
	}

	void printResult() {
		System.out.println("RESULT " + result);
	}
}

public class ServerClientPractice {
	public static void main(String[] args) { // client code : Calculator 코드를 이용
		Calculator calculator = new Calculator();
		calculator.plus(10, 20); 
		calculator.printResult(); // 30
		calculator.minus(10, 20);
		calculator.printResult(); // -10
		calculator.divide(20, 10);
		calculator.printResult(); // 2
		calculator.multiple(10, 20);
		calculator.printResult(); // 200
	}
}
```

---

### 캡슐화

> Client들은 Readme를 읽지 않는다 ⇒ Server Code Level에서 이를 제한해야 한다.
>

읽지 않는 Readme 내용

- 해당 클래스를 사용할 때, divide에 / 0 이 되지않도록 하시오.
- result 변수를 사용하지 마시오.

---

캡슐

- 데이터와 필드를 넣는다.
- 허용하는 데이터 / 필드로만, 데이터 제어 가능.
- 허용하지 않는 데이터 / 필드 접근 막음. 은닉한다.
- 캡슐화 장점 : server code가 허용한 방법대로 client code를 작성하도록 유도한다.

```java
class Calculator { // server code
	private int result; // client code에서 접근불가하도록 접근제한자 설정

	public void plus(int a, int b) {
		result = a + b;
	}

	public void minus(int a, int b) {
		result = a - b;
	}

	public void divide(int a, int b) {
		// client code에서 에러발생가능한 코드를 작성할 수 없도록 막아버림
		if (b == 0) {
			System.out.println("ERROR");
			return;
		}
		result = a / b;
	}

	public void multiple(int a, int b) {
		result = a * b;
	}

	public void printResult() {
		System.out.println("RESULT " + result);
	}
}

public class Second {
	public static void main(String[] args) { // client code
		Calculator calculator = new Calculator();
		calculator.divide(10, 0); // ERROR
	}
}
```

---

### 상속

- 부모가 가진 요소들을 자식들이 물려받아 사용가능.
- 코드 중복방지를 위해 공통적인 요소를 일반화시킨 것.
    - 코드 중복의 문제점 : 변경시 모두 다 한꺼번에 수정되지 X → 버그 유발.

---

Overloading / Overriding

- Overloading : Super class 메서드 재정의.
- Overriding : 같은 이름의 메서드이지만, 다른 argument로 함수 구분.
  - 메서드 시그니처(메서드명만 똑같다)가 다름 : 파라미터 타입, 개수

---

다형성

- 한 객체가 다양한 타입을 담을 수 있는 형태.
    - 상속 관계를 통해 다형성 구현가능.
- 하나의 명령으로 여러 구현부를 다룰 수 있다.

```java
class Robot {
	private int hp;

	public void move() {
		System.out.println("MOVE");
	}

	public void stop() {
		System.out.println("STOP");
	}
}

class SpeedRobot extends Robot {
	private int modelID;

	// Overring : superclass 메서드 재정의
	public void run() {
		System.out.println("FAST RUN");
	}

	// Overloading : 같은 이름의 메서드이지만, 다른 argument로 함수 구분
	public void run(int speed) {
		System.out.println("FAST RUN AS " + speed);
	}
}

public class Forth {
	public static void main(String[] args) {
		// 다형성 : speedRobot은 SpeedRobot도 될 수 있고, Robot도 될 수 있다
		SpeedRobot speedRobot = new SpeedRobot();
		// Robot을 상속받았다면, 공통적으로 사용가능한 메서드
		speedRobot.move(); // MOVE
		speedRobot.run(); // FAST RUN
		speedRobot.run(100); // FAST RUN AS 100
		// SpeedRobot에만 있는 고유 동작
 		speedRobot.stop(); // STOP
	}
}
```

---

### Interface

- 표준 규격을 만들어두고, 표준 규격을 사용하는 Server code를 구현해둔다.
- 이후, 어떤 Server code를 사용할지는 Client code에서 선택한다.
- 언젠가 추가될 유지보수를 위해 확장 가능한 형태로 만든다.
- 객체를 쉽게 사용하고자 표준화시킨다.

```java
interface Socket { // interface에 명시된 메서드는 반드시 구현해야 함
	void plugin();
	void unplug();
}

class Samsung implements Socket { // Samsung은 Socket interface의 규격을 따름(Realization)
	@Override
	public void plugin() {
		System.out.println("PLUGIN");
	}

	@Override
	public void unplug() {
		System.out.println("UNPLUG");
	}
}

public class Fifth {
	public static void main(String[] args) {
		Samsung samsung = new Samsung();
		samsung.plugin();
		samsung.unplug();
	}
}
```
