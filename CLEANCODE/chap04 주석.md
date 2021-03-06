# chap04 주석

잘달린 주석은 유용하지만, 근거가 없는 주석은 어렵게 만든다.

보통, 코드 의도를 표현 못해 주석을 사용한다. 표현력을 길러라

주석을 유지 보수하는건 어렵다.

부정확한 주석은 아예 없는 주석보다 훨씬 나쁘다

코드만이 정확한 정보를 제공하는 유일한 출처이다.



### 1. 주석은 나쁜 코드를 보완하지 못한다.

- 주석을 다는 이유는 코드 품질이 나쁘기 때문이다.
- 표현력이 풍부하고, 주석이 거의 없는 코드가 복잡하고 어수선하며 주석이 ㅁ낳이 달린 코드보다 좋다.



### 2. 코드로 의도를 표현해라

###### worst

```java
// 직원이 복지 혜택을 받을 자격이 있는지 검사한다.
if((employee.flags & HOURLY_FLAG) &&
   (employee.age >65 ))
```

###### best

```java
if(employee.isEligibleForFullBenefits())
```

### 3. 좋은 주석

어떤 주석은 꼭 필요하거나 유익하다.



*법적인 주석*

- 법적인 이유로 특정 주석을 넣으라고 명시한다.
- 소스 파일 첫머리에 추가한 표준 주석 헤더같은 경우



*정보를 제공하는 주석*

- 기본적인 정보를 주석으로 제공하면 편리하다.

###### example

```java
//test 중인 responder instance return
protected abstract Responder responderInstance();
// best
protected abstract Responder respondBeingTested();

// kk:mm:ss EEE, MMM dd, yyyy 형식
"정규표현식"
```

정규표현식에 대한 정보를 나타내는 주석. 하지만 클래스를 만들어 코드를 옮겨주면 더 깔끔하다.



*의도를 설명하는 주석*

결정에 깔린 의도를 설명해 주는 주석이 있다.

```java
return 1; // 오른쪽 유형이므로 정렬 순위가 더 높다.
```



*의미를 명료하게 밝히는 주석*

표준 라이브러리나 변경하지 못하는 코드라면, 명료하게 밝히는 주석이 유용하다.



*결과를 경고하는 주석*

결과를 경고할 목적으로 주석을 사용할 경우가 있다.

```java
// 여유 시간이 충분하지 않다면 실행하지 마세요!
```

`@Ignore` 을 사용하면 되지만, 위와 같은 주석은 적절하다.



*TODO 주석*

앞으로 할일을 남겨둔다.

당장 구현하기 어려운 업무를 기술한다.



*중요성을 강조하는 주석*

대수롭지 않게 넘기지 않기 위해 주석을 사용한다.



### 4. 나쁜 주석

*주절거리는 주석*

특별한 이유 없이 다는 주석. 저자는 이해하나, 보는 사람이 제대로 소통하지 못하면 나쁜 코드이다.



*같은 이야기를 중복하는 주석*

코드만 지저분하고, 정신없게 만든다

###### example

```java
/*
 * 이 컴포넌트의 프로세서 지연값
 */
protected int backgoundProcessorDelay = -1;

/*
 * 이 컴포넌트를 지원하기 위한 생명주기 이맨트
 */
protected LifecycleSupport lifecycle = new LifecycleSupport(this);
```



*오해할 여지가 있는 주석*

살짝 잘못된 정보로 인해, 다른 프로그래머가 잘못된 호출을 할 수 있음을 명심해라.



*의무적으로 다는 주석*

오히려 복잡하게 만든다. 코드만 헷갈리게 만들며, 잘못된 정보를 제공할 수 있다.



*이력을 기록하는 주석*

소스 코드 관리시스템을 사용해라. 세상좋아졌다



*있으나 마나 한 주석*

너무 당연한 사실을 언급하는 주석은 쓸 데 없다. 코드가 바뀌면 주석은 거짓말을 한다.



*무서운 잡음*

`javadocs` 도 잡음이 될 수 있다. 복붙하다 잘못 작성하는 경우도 존재한다.



*함수나 변수로 표현할 수 있다면 주석을 달지 마라*

주석을 달도록 코드를 개선해라.

*위치를 표시하는 주석*

###### example

```java
/////actions //////
```

특정 기능을 모아두면 유용한 경우도 있다.

일반적으로 가독성이 낮춘다. 

배너가 많을수록 가독성이 떨어진다.



*닫는 괄호에 다는 주석*

중첩이 심하고 장황하면, 닫는 괄호에 주석을 다는 경우가 생긴다.

주석을 다는 대신에, 함수를 줄이려 시도하자.



*공로를 돌리거나 저자를 표시하는 주석*

소스코드 관리 시스템에 저장해라



*주석으로 처리한 코드*

다른사람이 주석으로 처리한 코드는 지우기가 어렵다. 따라서 쌓여간다. 차라리 삭제해라.



*HTML 주석*

혐오 그자체.



*전역 정보*

근처에 있는 코드만 기술하고, 전반적인 정보를 기술하지 마라.



*너무 많은 정보*

불필요하다.



*모호한 관계*

주석과 주석이 설명하는 코드는 둘 사이 관계가 명백해야 한다.



*함수 헤더*

짧고 한가지만 수행하며 이름을 잘 붙힌 함수가 최고다.



*비공개 코드에서의 javadocs*

공개하지 않을 코드라면 쓸모가 없다.





