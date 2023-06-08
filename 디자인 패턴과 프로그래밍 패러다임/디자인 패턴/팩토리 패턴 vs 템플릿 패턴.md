# 팩토리 패턴 vs 템플릿 패턴
<br/>

## 개요
디자인 패턴을 공부하면서, 팩토리 메서드 패턴과 템플릿 메서드 패턴 개념이 혼동되었다.

따라서 각각의 개념과 차이, 헷갈린 이유와 별개의 개념인 이유를 정리해보았다.
<br/>
<br/>

## 팩토리 패턴
객체 생성을 하는 클래스를 따로 두는 것. 하위 클래스가 어떤 객체를 생성할지 결정하도록 위임하는 디자인 패턴
오버라이드된 메서드가 객체를 반환하는 패턴
템플릿 메소드 패턴을 활용한다.
 ![출처: https://western-sky.tistory.com/40](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbWJ4rH%2Fbtsiheme4El%2FX7xZX3ZdUhX92AgvsdNkJk%2Fimg.png)
<br/>
<br/>

## 템플릿 메서드 패턴
상속을 통해 부모클래스 기능을 확장할 때 사용하는 대표적인 방법
변하지 않는 기능은 부모에, 자주 변경되고 확장할 기능은 자식에 만든다.
부모에는 기본적인 로직과 그 기능의 일부를 추상 메소드나 오버라이딩이 가능한 메소드 등으로 만든다.
자식에는 부모에서 만든 메소드를 필요에 맞게 구현한다.
훅 메소드: 선택적으로 오버라이드할 수 있도록 만들어둔 메소드

![출처: https://western-sky.tistory.com/40](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbWJ4rH%2Fbtsiheme4El%2FX7xZX3ZdUhX92AgvsdNkJk%2Fimg.png)

여기서 Clerk 대신 커피 생성을 대신 해주는 Factory가 들어간다면 템플릿 메서드와 팩토리 메서드 패턴을 동시에 사용한 케이스가 될 것 이다. 
<br/>
<br/>

## 헷갈리는 이유?
팩토리 메서드 패턴을 구현할 때 필연적으로 부모-자식 클래스를 구현해야 하는데(예시: 커피 - 라떼, 아메리카노) , 이때 상속 시 상위 클래스의 메서드를 나누는 개념인 템플릿 메서드 패턴이 개입할 수 있으므로 같은 것으로 헷갈린 것 같다.

실제로는 팩토리 메서드 패턴은 생성 패턴에 속하고, 템플릿 메서드 패턴은 행위 패턴에 속하므로 유사한 패턴이라고 보기 어렵다.

다만 템플릿 메서드 패턴은 팩토리 메서드 구현 시에 개입될 여지가 있는 패턴이라고 볼 수 있을 것 같다.

![출처: https://western-sky.tistory.com/40](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fyj0Pi%2FbtsicPgm2lF%2FRD9gNcUExGeXIYO0O91GUK%2Fimg.png)
