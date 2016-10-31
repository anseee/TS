#Objective-C 2.0
지금까지 새 프로젝트들을 만들면서 책을 대충 보고 진행해온 내 스스로가 무언가 찜찜함이 계속해서 없어지질 않았다. 그래서 이번에 한번더 공부를 하려고 한다. 내가 만들었던 부분들 이해하지 못했던 부분들을 더 정리하는 차원에서 말이다. 시간 낭비일수도 있지만. Swift3.0까지 나온 상태이니까 말이다. 그렇다고 스위프트를 공부를 안하겠다는건 아니고, 둘다 공부할 생각이다. 

#Chapter01
1~2장, 4~6장은 정리하지 않았다.

##02 클래스, 객체, 메소드 
객체지향 프로그래밍의 핵심요들을 배워보자. 일단 객체란 무엇일까? 객체는 "어떤것이다". 객체지향 프로그래밍을 어떤 것이 있고 당신이 그것에 취하고 싶은 행동을 정하는 활동이라 할 수 있겠다. 무엇을 하고싶은지 부터 생각하고 객체에 대해 고민하지말자. 이것은 절차지향적인 옛날 생각에 불과하다.

그렇다면 예를 들어 다시 이야기 해보자. 실생활에서 자동차는 많이들 봤을것이다. 자동차가 객체이다. 그리고 우리가 보는 자동차는 인스턴스라 불리운다. 여기서 클래스란 용어를 말하고 싶은데, 클래스는 어떤 도면이라 생각하면 된다. 따라서 자동차란 클래스에서 새로운 인스턴스가 탄생하게 되는데, 이렇게 탄생하는 자동차들이 인스턴스이란 것이다. 이 인스턴스는 독립적이고 다양하게 사용자에 맞게 변경할 수 있다. 다시 정리해서 클래스에서 나온 것이 인스턴스이다. 또한 인스턴스가 수행하는 행동들을 '메서드' 라고 부른다.

Objective-C에서는 인스턴스에 메서드를 적용할 때 [ClassOrInstance method];와 같은 형태로 메시지를 보냈다고 표현한다.
그러면 한번 자동차를 생성해보자.

```Objective-C
Car *car = [Car new]; // 자동차를 하나 구입하자
```

위에서 new라는 메시지를 하나 보냈다. 이건 클래스에서 자동차 인스턴스를 하나 만들었다고 할 수 있겠다. 

자 그럼 클래스는 어떻게 만들 수 있을까?

###@interface
먼저 컴파일러에게 클래스가 어디서 왔는지 알려준다. 이것은 부모 클래스를 알려주어야 한다는 뜻이다. 두번째로 객체를 다룰 때 사용할 작업 혹은 메서드를 정의한다. 마지막으로 프로퍼티라는 항목을 나열한다. 

```Objective-C
@interface NewClassName : ParentClasName
	propertyAndMethodDeclarations;
@end

@interface XYPoint: NSObject

- (void)setX:(int)x;
- (void)setY:(int)y;
- (int)x;
- (int)y;

@end
```

###인스턴스 메소드와 클래스 메소드
메소드 앞에 -를 볼 수 있겠다. 이 표현은 인스턴스 메소드를 표현 하며, 인스턴스 메서드는 클래스의 특정 인스턴스에 작업을 수행한다. 
+는 클래스 메소드라 불리우며, 클래스 자체에 직업을 수행한다. 

###@implement
interface안에서 선언한 메서드의 실제 코드를 담고 있다. 또한 클래스의 객체가 담을 데이터의 종류도 여기에서 담는다. 

```Objective-C
@implementation XYPoint
{
    int x; // 인스턴스 변수
    int y;
}

- (void)setX:(int)tempX {
    x = tempX;
}

- (void)setY:(int)tempY {
    y = tempY;
}

- (int)x {
    return x;
}

- (int)y {
    return y;
}

@end
```

###Alloc과 init
alloc은 allocate(할당하다)의 줄임말이다. 객체를 생성하는데 있어서 alloc이란 메시지를 보내면 객체에 필요한 메모리 공간을 할당 하는것이다. Init 메서드는 클래스의 인스턴스를 초기화한다. 이것은 클래스가 아니라 특정 객체를 초기화 하는것을 뜻한다. 

과거에는 객체의 사용이 끝나면 Release란 명령어를 통해서 객체의 사용이 끝났음을 알려줘야한다. 이것이 수동 레퍼런스 카운팅이라고 불리는 메모리 관리 시스템을 지켜주기 위해서였다. Xcode4.2부터 프로그래머가 신경쓸 필요가 없어졌다. 자동 레퍼런스 카운팅 ARC 기법이다. 

인스턴스 선언시 변수 앞에 *을 붙이는것을 보았을것이다. 이것은 객체의 참조를 의미한다. 이것은 실제 데이터를 저장한것이 아니라. 객체의 데이터가 메모리에서 어디에 위치하고 있는지에 대한 메모리 주소를 갖고 있다. alloc을하면 각 인스턴스 객체에 0이 체워저 있고 init을 하면 인스턴스 변수에 실제 값들이 초기화된다. 

###인스턴스 변수 접근과 데이터 캡슐화
인스턴스 메서드는 언제나 자신의 인스턴스 변수에 직접 접근할 수 있다. 그러나 클래스 메서드는 클래스의 인스턴스가 아닌 클래스 자신만 다루기 때문에 implement안에서 선언된 변수들에 접근이 불가능하다. 변수에 직접적으로 접근하는것은 불가능하다 변수는 숨겨져 있기 때문이다. 이 개념은 데이터 캡슐화의 핵심 요소다. 클래스 내부 정보를 수정할지 말지를 걱정하지 않고 클래스의 정의를 확장하거나 수정하도록 해줄 수 있다. 또한 프로그래머와 클래스 개발자 사이에 적절한 분리층이 생긴다.

인스턴수 변수를 가져오거나 설정하기 위해서는 인스턴스 메소드를 이용해서 가져오거나 설정할 수 있다. 이때 사용하는 메서드를 게터와 세터란 용어로 불리운다. 이 두 용어를 합쳐 접근자 메서드라고 불리운다. 세터는 인자를 받아 해당 인스턴스 변수에 인자값을 대입하는 목적이고 게터는 저장된 인스턴스 변수의 값을 가져오는것이다. 변수의 직접적으로 접근해서 설정하거나 값을 가져오는것은 불가능하고 게터와 세터를 작성해서 사용해야하는 것이 데이터 캡슐화의 핵심.

###마무리
이 장에서는 자신만의 클래스를 정의하고 인스턴스를 생성해 메시지 보내는 방법을 배웠다. 