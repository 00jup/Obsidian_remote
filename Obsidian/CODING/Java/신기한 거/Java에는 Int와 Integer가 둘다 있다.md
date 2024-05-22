
최근에 자바를 공부하고 있는데,

공부하면서 이상한 점을 발견했다. 파이썬에서는 고민조차 안했던 건데;;;

int와 Integer는 대체 무슨 차이일까?

자바 코드 아키텍처도 살짝 다르게 작성하던데 왜 굳이 저거처럼 다르게 쓸까? 의미는 똑같아 보이는데;;

## **1. int**

먼저, Int는 Primitive 자료형이다. 즉, 변수의 타입(data type) 이다.

> Primitive  
> - 데이터를 가지는 자료형을 뜻하는 원시적이 자료형.  
> - 메소드를 가지지 못한다.

앞서 변수의 타입으로 표현하였는데. 변수는 값을 저장할 수 있는 메모리 상의 공간을 의미한다.

int a = 3;

char firstName = "H";

에서 a나 firstName은 변수가 되는 것이다.

그리고 그 앞에 적힌 int나 char가 변수의 형을 지정해주고 있는 것이, 변수의 타입이라고 한다.

즉, 이렇게 정리해볼 수 있다.

**자료형은 'data의 type에 따라 값이 저장될 공간의 크기와 저장 형식을 정의한 것'** 이라고 볼 수 있다.

![](https://blog.kakaocdn.net/dn/kQi9P/btrUTJYfPln/b9NFPNnKKkdr1gZ1Cvc5KK/img.png)

## **2. Integer**

변수를 선언할 때, int는 굉장히 자주 쓴다. 

그러면 Integer는 우리가 평소에 어디에서 자주 사용할까?

```
	ArrayList<Integer> intList = new ArrayList<Integer>();
	intList.add(1);
	intList.add(2);
	System.out.println(intList.get(0));
```

```
	String stringNum = "123";
	int intNum = Integer.parseInt(stringNum);
	System.out.println(intNum);
```

아마 위와 같으 상황에서 자주 사용할 것이다.

> - 매개변수로 객체를 필요로 할 때  
> - 기본형 값이 아닌 객체로 저장해야할 때  
> - 객채 간 비교가 필요할 때

위와 같을 때 자주 사용한다. 

무엇을..?

Integer와 같은 래퍼 클래스(wrapper class)를 말한다.

> 래퍼 클래스(wrapper class)  
> 객체가 기본 데이터 유형을 래핑하거나 포함하는 클래스

래퍼 클래스를 이용하면 객체를 만들 때 필드를 포함하고 이 필드에 기본 데이터 유형을 저장할 수 있다.

그렇다면 Integer는 int의 래퍼 클래스를 의미한다는 것이다.

![](https://blog.kakaocdn.net/dn/XCr2l/btrUV4OmO6h/0Jvik596G6yA7W33LanugK/img.jpg)

## **3. int 와 Integer의 차이점**

**int는 자료형**

- 산술 연산 가능
- null로 초기화 불가능
- 저장공간이 4Byte라고 작음

**Integer**

- Unboxing하지 않을 시 산술 연산이 불가능
- null 값으로 처리 가능
- 저장공간이 큼
- null값으로 처리가 가능해 SQL에 용이하게 쓰인다.

## **4. 어떤 상황에서 사용하면 될까?**

프로그램에 무리가지 않기 위해 int를 사용한다. 용량이 더 작고 null값이 들어오지 못하니 값이 없을 땐 에러를 발생시키니깐.

그럼 Integer는?

null 또는, 데이터를 wrapper 할 경우에 사용한다.