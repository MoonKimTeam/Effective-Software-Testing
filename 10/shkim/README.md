# 테스트 코드 품질

## 테스트 코드의 유지 보수성을 위한 원칙

### 테스트는 빨라야 한다

소스 코드를 유지보수하거나 변경을 할때마다 우리는 시스템이 기대한대로 동작하는지 테스트 스위트로부터 피드백을 받는다. <br>
테스트 스위트가 느리면 테스트를 덜 하게 되고, 그러면 테스트 스위트가 효율적이지 않게 된다. <br>
만약 어떤 테스트가 느리다면 다음 사항을 고려해보자.

- 모의 객체나 스텁을 이용해서 테스트의 일부 느린 구성요소를 대체한다.
- 제품 코드를 재설계해서 느린 코드를 빠른 코드와 분리하여 테스트할 수 있도록 한다.
- 느린 테스트를 자주 실행하지 않는 다른 테스트 스위트로 옮긴다.

### 테스트는 응집력있고 독릭접이며 격리되어야 한다

테스트는 다른 테스트의 결과에 의존하면 안되고, 테스트 결과는 테스트를 격리해서 실행하든 테스트 스위트에 있는 나머지 테스트와 함께 실행하든 항상 같아야 한다. <br>
테스트 A의 작업이 테스트 B의 환결설정에 의존하는 경우는 테스트 신뢰도가 매우 떨어진다.

### 테스트는 존재 이유가 있어야 한다

테스트가 존재해야 할 타당한 이유가 없다면 존재하지 말아야 한다. <br>
모든 테스트는 유지보수되어야 한다는 것을 기억하자

### 테스트의 단언문은 탄탄해야 한다

테스트는 수행한 코드가 예상대로 동작했다고 단언하기 위해 존재한다. 그러므로 단언문을 잘 작성해야 좋은 테스트를 만들 수 있다. <br>
단언문은 테스트의 행위의 유효성을 완전히 검사하고, 출력에 약간의 변화가 생기면 중단되어야 한다.

### 테스트는 행위가 변경될 경우 깨져야 한다

행위가 깨졌는데 테스트 스위트가 여전히 초록불이라면 테스트에 문제가 있는 것이다. <br>
이러한 현상은 약한 단언문이나 메서드는 수행되지만 테스트가 제대로 되지 않아 발생할 수 있다.

<br>

## 테스트 냄새

### 과다한 중복

중복 코드는 소프트웨어 개발자의 생산성을 떨어뜨릴 수 있다. 만약 중복된 코드를 수정해야 한다면 코드가 중복된 모든 장소에 동일한 변경사항을 적용해야 한다. <br>
테스크코드를 자주 리팩토링하고, 중복 코드를 private 메서드나 외부 클래스로 추출하는 것은 문제를 빠르고 저렴하게 해결하는 좋은 방법이다.

### 불명확한 단언문

어떤 기능이나 비즈니스 규칙은 너무 복잡해서 행위를 확인하기 위해 복잡한 단언문 집합이 필요하다. <br>
결국 이해하기 어려운 단언문을 작성하게 된다. 이런 경우 단언문의 복잡성 일부를 추상화하는 맞춤형 단언문을 작성하고, 단언문의 내용을 자연어로 설명하는 주석을 달아두자.

### 복잡하거나 외부에 있는 자원에 대한 잘못된 처리

외부 자원을 사용하는 테스트코드를 이해하는 일은 어려울 수 있다. <br>
테스트에서 자원이 이미 올바른 상태에 있다고 가정하면 안되고, 테스트는 상태를 설정하는 책임을 져야한다. <br>
즉 테스트가 데이터베이스에 데이터를 채우고, 필요한 파일을 디스크에 쓰고, 톰캣 서버를 실행하는 작업을 책임져야 한다.

### 너무 범용적인 픽스처

테스트의 픽스처가 가능한 한 구체적이고 응집되어 있는지 확인하는 일은 테스트의 본질을 이해하는데 도움이 된다. <br>
빌더 패턴을 사용하여 범용 픽스터 작성을 피할 수 있다.

### 민감한 단언문

단언문이 너무 민감한 것은 아닌지 확인하자. 그렇지 않으면 테스트가 적합한 이유 없이 깨질 수 있다.



















