# UML

---

### UML(Unified Modeling Language)

- Modeling : 모델, 모형, 가짜.
- Language : 언어 → 의사소통의 수단.
- 객체지향 설계의 표준 표기법 : 공통된 표준 표기법.
- 추상화 : 복잡도를 낮춰주고 중요한 부분을 드러낸다 ⇒ 시스템을 이해하기 쉽게 해주고, 의사소통에 기여할 수 있다.

---

### UML 특징

의사소통을 위한 도구

- 필요한 View만 시각화하여 이해하기 쉽도록 보여준다.
- 공통된 표준 언어로서 의사소통에 기여한다.

모델링 언어

- 여타 다른 모델, 모형들과 마찬가지로 실제 만들어 보는 것과 모델을 만드는 것의 비용을 생각해볼 수 있다.

---

### UML의 쓰임새

코드보다 모델이 효율적인 경우

- 시각화를 통한 시스템 이해도 높이기.
- 코드 작성 비용 > 모델 작성 비용.

조직과의 의사소통

- 같은 조직 내 오해 방지.
- 다른 조직과의 의사소통.
- 문서를 통한 정확한 의사소통.

기획 산출물이 완료되었다는 증거

- 인증이 필요한 분야( 임베디드, 항공, 대규모 프로젝트 )에서 필수 항목.

---

### UML 다이어그램 종류

![Untitled](UML%2046d90f06a0ac41358902288cedd485e2/Untitled.png)

1. struct diagrams( 정적 )
- 시간에 상관없는 정적인 구조를 나타낸다.
- Class Diagram.

1. behavior diagrams( 동적 )
- 시간에 따라 변경이 일어나는 것을 표현하기 위함.
- Use Case Diagram.
- Activity.
- State Machine.
- Sequence Diagram.

---

### Class Diagram

![Untitled](UML%2046d90f06a0ac41358902288cedd485e2/Untitled%201.png)

- 클래스의 속성(attribute), 기능(operation)을 표현한다.

![Untitled](UML%2046d90f06a0ac41358902288cedd485e2/Untitled%202.png)

- 클래스 끼리의 정적인 관계를 표현한다.
- UML 표준 규칙 :
    - 클래스 이름은 대문자로 시작.
    - 메서드와 필드는 모두 소문자로 시작.
    - 메서드 이름은 동사로 시작.
- Scope :
    - \+ : public.
    - \- : private.
  - \# : protected.
- stereotype :
    - 기존의 표기법을 재활용( 확장 )해서 새로운 의미를 부여한다.
    - `<< 새로운 의미 부여 >>` 형태로 쓴다.
    - 대표적으로 interface 표기.

![Untitled](UML%2046d90f06a0ac41358902288cedd485e2/Untitled%203.png)

```java
public interface Vehicle {
	public void start();
	public void stop();
	public void accelerate();
}

class Car implements Vehicle {
	@Override
	public void start() {}

	@Override
	public void stop() {}

	@Override
	public void accelerate() {}
}

class Bike implements Vehicle {
	@Override
	public void start() {}

	@Override
	public void stop() {}

	@Override
	public void accelerate() {}
}
```

---

### Coupling( 결합도 )

클래스에서 의존 :

![Untitled](UML%2046d90f06a0ac41358902288cedd485e2/Untitled%204.png)

- A클래스가 B클래스가 없으면 안되는 상황.
- B클래스를 변경하면 A클래스를 변경해야할 수도 있음.
- 의존성 **∝** 변경정도.
- 결합도 : 의존하는 정도.

> 변경이 많은 부분에 직접적으로 의존하지 않도록( **loose coupling** ) 하자.
>

---

### Class Diagram 관계

1. Realization( 구현화 ) : Interface를 실제로 구현.
2. Generalization( 일반화 ) : 공통적인 것을 추출하여 분류를 만들어 냄.
3. Dependency
- 외부 클래스를 임시적으로 사용하는 관계.
- 클래스가 참조를 유지하지 않음.
- Dependency의 기본적인 3가지 형태 :

  (1) Local

![Untitled](UML%2046d90f06a0ac41358902288cedd485e2/Untitled%205.png)

(2) Parameter

![Untitled](UML%2046d90f06a0ac41358902288cedd485e2/Untitled%206.png)

(3) Factory

![Untitled](UML%2046d90f06a0ac41358902288cedd485e2/Untitled%207.png)

![Untitled](UML%2046d90f06a0ac41358902288cedd485e2/Untitled%208.png)

```java
class Factory {
	// Figure의 생성자 역할을 대신한다
	// 지역변수로 객체생성만 하므로 참조관계 유지 X
	public Figure make(String name) {
		return new Figure(name);
	}
}

class Figure {
	private String name;

	public Figure(String name) {
		this.name = name;
	}

	public void play() {
		System.out.println(this.name + " PLAY");
	}
}

public class Main01 {
	public static void main(String[] args) {
		Factory factory = new Factory();

		Figure 손오공 = factory.make("손오공");
		Figure 치치 = factory.make("치치");
		Figure 부우 = factory.make("부우");

		손오공.play();
		치치.play();
		부우.play();
	}
}
```

1. Association

![Untitled](UML%2046d90f06a0ac41358902288cedd485e2/Untitled%209.png)

- 다른 클래스를 사용하는데, 참조를 유지하는 방식.

> Dependency vs Association
다른 객체를 **일시적 ↔ 지속적** 으로 사용하는 관계
>

5. Aggregation

- Association과 구분이 확실치 않음.
- Aggregation은 Association이라고 불러도 됨.

1. Composition

![Untitled](UML%2046d90f06a0ac41358902288cedd485e2/Untitled%2010.png)

- 함께 생성되며, 함께 소멸되는 관계.
- 반드시 존재해야만 하는 관계.

---

### Interface와 의존성

Interface가 변경되면?

- 변경이 크게 일어난다.
- 하지만, Interface가 바뀔 일은 흔하지 않음.

### 상속과 의존성

부모가 변경되면?

- 변경이 크게 일어난다.
- 의존성이 매우 크다.

---

### Sequence Diagram

![Untitled](UML%2046d90f06a0ac41358902288cedd485e2/Untitled%2011.png)

- 여러 객체들이 어떻게 상호작용 하는지를 나타내는 다이어그램.
- 시간순서를 나타낸다(위 → 아래).
- 객체끼리의 상호작용을 시간 순서대로 보여준다.

---

1. Actor : 등장인물.
2. Lifeline : 생명선( 시간이 흐르고 있음을 나타냄 ).
3. Message : 시간 순서대로 메시지를 추가.
4. Return Message : 메시지에 대한 응답 추가( 점선 ).
5. alternative frame : 분기지점

![Untitled](UML%2046d90f06a0ac41358902288cedd485e2/Untitled%2012.png)

1. Activation Box : 객체가 활성상태인지 아닌지 여부를 나타냄.

![Untitled](UML%2046d90f06a0ac41358902288cedd485e2/Untitled%2013.png)

---

### UseCase Diagram

![Untitled](UML%2046d90f06a0ac41358902288cedd485e2/Untitled%2014.png)

- 요구사항을 파악하는 용도.
- 요구사항을 개념화하는 목적.
- UseCase는 철저히 Client 기준 ⇒ 어떤 것이 필요한지만 기술( 구현방법X ).

---

작성방법

1. Actor 정의 : 시스템 외부의 관련자로, 사람이름이 아닌 역할을 지정해야함.
2. UseCase : 동사로 필요한 기능( 요구사항 ) 나열.
3. 관계선 : 각 동작과 Actor 간의 관계를 선으로 표현.
    - Generalization.
    - include 관계 : 반드시 이루어져야 하는 관계 표현.
    - extends 관계 : 반드시 이루어지지 않고, 특정 조건이 발생시 수행되는 Case( 조건도 함께 추가 ).
