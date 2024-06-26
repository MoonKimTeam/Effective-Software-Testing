# 명세 기반 테스트

명세 테스트의 개념 요구사항 자체에서 테스트를 도출하는 것이다.

## 요구사항이 모든 걸 말한다

예를 들어, 오늘 새로운 요구사항을 받았다. 요구사항 분석을 시작하자마자 구현할 어떤 메서드를 뽑아냈다. <br>
이 메서드는 주어진 문자영ㄹ에서 두 태그 사이에 존재하는 모든 부분 문자열을 반환한다. 이 메서드를 **substringsBetween()** 이라고 하자. <br>
**substringsBetween()** 메서드에 대해 다음과 같은 요구사항을 도출했다.

> 어떤 문자열에서 start와 end 태그로 구분되는 부분 문자열을 모두 찾아서 배열로 반환한다. <br>
> str: 주어진 문자열. null일경우 null을 반환. 빈 문자열일 경우 빈 배열을 반환 <br>
> open: 찾으려는 문자열의 시작을 가리치는 문자열. 빈 문자열일 경우 null을 반환 <br>
> close: 찾으려는 문자열의 끝을 가리키는 문자열. 빈 문자열이면 null을 반환

### 1단계: 요구사항과 입출력에 대해 이해하기

요구사항을 어떻게 작성했든, 그것은 세 부분으로 이루어져 있다.

1. 메서드는 무엇을 수행해야 하는가
2. 프로그램은 데이터를 입력으로 받는다
3. 출력에 대한 추론은 프로그램이 무엇을 수행하고 입력이 어떻게 기대하는 출력으로 변환되는지 더 잘 이해하도록 해준다.

substringsBetween() 메서드의 경우 다음과 같다

1. 이 메서드의 목표는 문자열에서 open과 close 태그로 구분된 모든 부분 문장열을 모으는 일이다.
2. 프로그램은 세 종류의 매개변수를 받는다.
   1. 프로그램이 부분 문자열을 추출해낼 대상 문자열인 str
   2. 부분 문자열의 시작을 나타내는 open 태그
   3. 부분 문자열의 끝을 나타내는 close 태그
3. 프로그램은 찾아낸 모든 부분 문자열을 배열로 반환한다.


### 2단계: 여러 입력값에 대해 프로그램이 수행하는 바를 탐색하기

여러 문자열을 넣어보며, 내가 원했던 결과를 되돌려주는지 테스트해본다. <br>
머릿속에 메서드가 어떻게 동작해야 할지에 대한 명확한 그림을 가지게 되면 탐색 단계를 멈춘다.

### 3단계: 테스트 가능한 입출력과 구획을 탐색하기

우리는 프로그램의 정확성을 충분히 확신할 수 있도록, 입출력에 대해 우선순위를 매기고 그 일부를 선택하는 방법을 찾아내야 한다. <br>
이러한 탐색을 체계적으로 하는 방법은 다음과 같이 생각하는 것이다.

1. 각각의 입력에 대해: '내가 전달하는 입력이 어떤 부류에 해당하는가 ?'
2. 각 입력과 다른 입력의 조합에 대해: 'open 태그와 close 태그 사이에 어떤 조합을 만들 수 있을까 ?'
3. 이 프로그램에서 기대하는 여러 부류의 출력에 대해: '배열을 리턴하는가 ? 빈 배열을 리턴할 수 있을까 ? null을 리턴할 수 있을까 ?'

### 4단계: 경계 분석하기

버그는 경계를 좋아하므로 이 부분을 철저히 해야 한다. <br>
이전 단계에서 고안한 모든 구획이 가진 경계를 분석한다. 관련성이 있는 테스트를 식별해서 목록에 추가한다.

### 5단계: 구획과 경계를 기바느로 테스트 케이스 고안하기

기본 아이디어는 모든 가능한 입력 조합을 테스트하기 위해 서로 다른 범주에 있는 모든 구획을 조합하는 것이다. <br>
하지만 모든 것을 조합하는 일은 비용이 많이 들기 때문에, 일반적으로 예외 케이스는 단 한 번만 테스트하고 다른 구획과 조합하지 않는 방법이 있다.

### 6단계: 테스트 자동화하기

고안한 테스트 케이스를 자동화된 테스트로 작성하는 일이다. <br>
테스트에 사용할 구체적인 입력값을 식별하고, 프로그램 수행 결과에 대한 기댓값을 명시하는 일을 말한다.

### 7단계: 창의성과 경험으로 테스트 스위트를 강화하기

놓친 케이스가 없는지, 어떤 케이스에서 실패할 거라고 느껴지는지 등을 생각한다.

<br>

## 현업에서의 명세 테스트

### 명세 테스트는 어느 정도로 수행해야 하는가 ?

프로그램이 어떤 부분에서 실패하면 비용이 얼마나 들지 생각한다. <br>
비용이 높은 경우라면 테스트에 더 투자를 하고, 더 많은 코너 케이스를 탐색하고, 품질을 보장하기 위해 다양한 기술을 시도하는 것이 현명할 수 있다.

### 이해를 높이기 위해 입력을 변경해서 사용하자

입력 공간을 살펴보고 코너 케이스를 식별하기 위해 다양한 입력은 필수다. <br>
구획을 엄격하게 식별해서 테스트에 집중해야 한다.

### null과 예외 케이스는 의미가 있을때만 사용하자

테스트 중인 코드가 UI와 매우 관련이 있는 경우라면 null, 빈 문자열, 일반적이지 않은 정숫값 등과 같은 코너 케이스를 많이 수행해야 한다. <br>
코드가 UI와 별로 관련이 없고 테스트 대상 구성 요소에 도달하기 전에 검사된 것이 확실하다면 이러한 테스트를 건너뛸 수 있다.

### 이것은 클래스와 상태에 어떻게 동작하는가 ?

객체 지향 시스템에서 클래스는 상태를 가진다. ShoppingCart 클래스와 totalPrice() 동작을 상상해보자. <br>
totalPrice()는 작업을 수행하기 전에 CartItem 몇 개를 삽입해야 한다. <br>
totalPrice()의 예상 동작은, 카트에 품목 종류가 0개, 1개, 여러 개인 경우, 품목의 수량이 다수인 경우일 때 메서드의 동작을 수행하는 테스트를 상상해볼 수 있다.
























