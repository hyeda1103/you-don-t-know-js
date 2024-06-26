# 클래스와 객체의 혼합

- 클래스와 객체 지향 프로그래밍 `Object-Oriented Programming`에 대해 알아보자
- 사실 클래스 지향 개념은 자바스크립트 객체 체계와는 잘 맞지 않는다

## 4.1 클래스 이론
- 클래스와 상속은 실생활 영역의 문제를 소프트웨어로 모델링하기 위한 방법이다.
  - 객체 지향 프로그래밍에서 데이터는 자신을 기반으로 하는 실행되는 작동과 연관되므로 데이터와 작동을 함께 잘 감싸는 (캡슐화, `capsulation`) 것이 올바른 설계라고 강조한다.
- 클래스는 특정 자료 구조를 분류하는 용도로 쓴다. 흔히 인용하는 예로, 차 `Car`는 일반적인 탈것 `Vehicle` 클래스의 구현체 중 하나다.
  - 다른 탈것마다 '사람을 운송하는 기능'을 매번 재정의해야 한다면 올바른 소프트웨어 설계가 아닐 것이다. 그래서 `Vehicle`을 한곳에 정의해두고 `Car`는 `Vehicle`에 있는 기반 정의를 상속 `Inherit`받아 정의한다.
- **다형성 `Polymorphism`**은 또 다른 클래스의 핵심 개념으로 부모 클래스에 뭉뚱그려 정의된 작동을 자식 클래스에서 좀 더 구체화하여 오버라이드(재정의)하는 것을 뜻한다.

### 4.1.1 클래스 디자인 패턴
- 순회자, 관찰자, 팩토리, 싱글턴 등의 유명한 객체 지향 디자인 패턴들이 있는데, **클래스 역시 디자인 패턴의 일종**이다.

### 4.1.2 자바스크립트 클래스
- 자바스크립트는 클래스와 비슷하게 생긴 구문 요소도 갖추고 있고 최근 `ES6`부터는 아예 `class`라는 키워드가 명세에 정식으로 추가왰다.
  - **그럼 자바스크립트는 클래스가 있는 것일까?**
  - **단도직입적으로 말해서 "아니다"**
- 클래스는 디자인 패턴이므로 고전적인 클래스 기능과 얼추 비슷하게 만들어볼 수는 있겠지만, 이는 클래스처럼 보이는 구문일 뿐이며 개발자들이 클래스 디자인 패턴으로 코딩할 수 있도록 자바스크립트 체계를 억지로 고친 것에 불과하다. 

## 4.2 클래스 체계
### 4.2.1 클래스와 인스턴스
- 개발자가 상호작용할 실제 객체는 클래스라는 붕어빵 틀에서 구워낸다 (인스턴스화한다). 이렇게 구워낸 결과가 인스턴스라는 객체고 개발자는 객체 메서드를 직접 호출하거나 공용 `Public` 데이터 프로퍼티에 접근한다. 객체는 클래스에 기술된 모든 특성을 그대로 가진 **사본**이다. 즉 클래스는 복사 과정을 거쳐 객체 형태로 인스턴스화한다.
### 4.2.2 생성자
- 생성자는 클래스에 속한 메서드로, 클래스명과 같에 명명하는 것이 일반적이다.
- 클래스 인스턴스를 생성할 거라는 신호를 엔진이 인지할 수 있도록 항상 `new` 키워드를 앞에 붙여 생성자를 호출한다.

## 4.3 클래스 상속
- 클래스 지향 언어에서는 자체로 인스턴스화할 수 있는 클래스는 물론이고 첫번째 클래스를 상속받은 두번째 클래스를 정의할 수 있다. 이때 첫번째를 `Parent Class` 두번째를 `Child Class`라고 통칭한다.
- `Child Class`는 `Parent Class`에서 완전히 떨어진 별개의 클래스로 정의된다. 부모로부터 복사된 초기 버전의 작동을 고스란히 간직하고 있지만 물려받은 작동을 전혀 새로운 방식으로 오버라이드할 수 있다.

### 4.3.1 다형성
- 클래스를 상속하면 `Child Class`에는 자신의 `Parent Class`를 가리키는 상대적 레퍼런스가 주어지는데, 바로 이 레퍼런스를 보통 `super`라고 한다.
  - `Child Class`가 `Parent Class`에 연결된 양 혼동하면 안된다. 클래스 상속은 한마디로 복사다.
### 4.3.2 다중 상속
- 일부 클래스 지향 언어에서는 복수의 `Parent Class`에서 상속받을 수 있다. 다중 상속은 `Parent Class` 각각의 정의가 `Child Class`로 복사된다는 의미다.
- (자바스크립트는 다중 상속 기능 따위는 아예 처음부터 지원하지 않았다.)

## 4.4 믹스인
- `Mixin`은 다른 언어와 달리 자바스크립트에선 누락된 클래스 복사 기능을 흉내낸 것으로 명시적 믹스인과 암시적 믹스인 두 타입이 있다.
### 4.4.1 명시적 믹스인
- 믹스인 함수는 `sourceObj` 프로퍼티를 순회하면서 `targetObj`에 같은 이름의 프로퍼티 유무를 체크하여 없으면 복사한다.
- 사실 자바스크립트 함수는 표준적인 방법으로 복사할 수 없다. 복사되는 건 같은 공유 함수 객체를 가리키는 사본 레퍼런스다. 공유 함수 객체에 프로퍼티를 추가하는 등의 변경을 하면 공유 레퍼런스를 통해 모두에게 영향을 준다.
- 실제로 어떤 객체에서 다른 객체로 프로퍼티를 복사하느니 차라리 그냥 무식하게 똑같은 프로퍼티를 각각 두번씩 정의하는 편이 더 낫다. 명시적 믹스인은 코드 가독성에 도움이 될 때만 조심하여 사용하되 **객체 간 의존 관계가 난해하게 양산될 기미가 보이면 사용을 중단하기 바란다.**

## 4.5 정리하기
1. 클래스는 디자인 패턴의 일종이다.
2. 자바스크립트에서 클래스의 의미는 다른 언어에서의 클래스와 다르다.
3. 클래스틑 복사를 의미한다.
4. 자바스크립트는 객체 간 사본을 자동으로 생성하지 않는다.
5. 믹스인 패턴은 클래스의 복사 기능을 모방하기 위해 종종 쓰이지만 대부분 명시적 의사다형성처럼 보기 싫고 취약한 구문이 되어 유지 보수가 어렵고 가독성도 떨어지는 코드가 된다.
6. **일반적으로 자바스크립트에서 클래스를 모방하는 건 당장 닥친 문제를 해결할 수는 있어도 앞으로 터질 시한폭탄을 심어놓는 것과 같다.**
