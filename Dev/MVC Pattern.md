# MVC Pattern

MVC Pattern 은 사용자 인터페이스, 데이터 및 제어 논리를 구현하는데 일반적으로 사용되는 소프트웨어 아키텍처 패턴이다. 소프트웨어를 3개의 영역으로 나누어 비즈니스 로직과 디스플레이 영역을 분리해 서로 영향을 주지 않고 유지보수가 가능하다.

## MVC Pattern 의 구조

![image](https://user-images.githubusercontent.com/66311161/193447290-27d062cb-ce22-4555-a139-c2491ac8f82f.png)

 MVC Pattern 은 모델(model), 뷰(view), 컨트롤러(Controller) 세 개의 컴포넌트로 이루어져 있고 각 컴포넌트별로 고유한 역할을 수행한다.

### 1. 모델(Model)

모델은 앱에 포함되어야 하는 데이터를 정의한다. 비즈니스 로직을 처리한 후 모델의 변경사항을 뷰와 컨트롤러에 전달한다. 

모델은 다음과 같은 규칙을 가진다.

- 사용자가 편집하길 원하는 모든 데이터를 가지고 있어야 한다.
- 변경이 일어나면, 변경 통지에 대한 처리 방법을 구현해야만 한다.

### 2. 뷰(View)

뷰는 앱의 데이터가 표시되는 방식(User Interface)을 정의한다. MVC Pattern은 여러개의 뷰가 존재할 수 있으며, 모델에게 질의하여 데이터를 전달받는다. 

뷰는 모델에게 전달받는 데이터를 화면에 표시하는 역할을 가지고 있으며, 사용자가 화면에 표시된 내용을 변경하게 되면 모델에게 전달하여 모델을 변경해야 한다. View를 업데이트하기 위해서는 다음과 같은 방법이 있다.

- View가 Model을 직접 이용하여 업데이트
- Model에서 View를 Notify 하여 업데이트
- View가 Polling하여 Model의 변화를 감지해서 업데이트

뷰는 다음과 같은 규칙을 가진다.

- 모델이 가지고 있는 정보를 따로 저장해서는 안된다.
- 변경이 일어나면 변경통지에 대한 처리방법을 구현해야 한다.

### 3. 컨트롤러(Controller)

컨트롤러는 사용자의 입력에 대한 응답으로 모델, 뷰를 업데이트하는 방법을 정의한다. 모델이나 뷰는 서로의 존재를 모르고 있다. 변경사항을 외부로 알리고 수신하는 방법만 정의되어 있을 뿐이다. 컨트롤러는 이를 중재하기 위해 모델과 뷰에 대해 알고있어야 한다. 모델이나 뷰로부터 변경 내용을 통지 받으면 이를 각 구성에 요소에게 통지한다.

컨트롤러는 다음과 같은 규칙을 가진다.

- 모델이나 뷰에 대해서 알고 있어야 한다.
- 모델이나 뷰의 변경을 모니터링 해야 한다.

## MVC Pattern 의 사용

MVC Pattern의 가장 매력적인 요소는 관심사 분리이다. 대규모의 웹 앱은 매우 복잡하고 유지보수가 큰 골칫거리인 경우가 많다. 따라서 프론트엔드와 백엔드를 별도의 구성 요소로 관리하면 애플리케이션을 쉽게 유지 관리하고 확장할 수 있다. 결국 MVC Pattern 을 사용하는 이유는 유지보수의 편리성 때문이다. MVC Pattern을 가진 시스템의 각 컴포넌트는 자신이 맡은 역할만 수행한 후 다른 컴포넌트로 결과만 넘겨주면 되기 때문에 시스템 결합도를 낮출 수 있다. 유지보수 시에도 특정 컴포넌트만 수정하면 되기 때문에 보다 쉽게 시스템 변경이 가능하다.

- ### MVC Pattern 의 적용 사례

MVC Pattern은 Spring, Django 등의 프레임워크와 JSP를 사용한 웹 어플리케이션 개발에서 가장 즐겨 사용되는 개발 방식이다. 

1. 브라우저 화면에서 서버로 데이터를 전달한다.
2. 컨트롤러에서 데이터를 전달받아 서비스에게 데이터를 전달한다.
3. 서비스는 JPARepository를 이용하여 전달받은 데이터를 데이터베이스에 INSERT 한다.
4. INSERT 수행 후 컨트롤러는 서비스를 통해 데이터를 다시 조회한다.
5. 조회한 데이터를 모델 객체를 통해 뷰에게 전달한다.
6. 화면에 변경이 발생하는지 확인한다.

## MVC Pattern 의 한계

세상에 완벽한 설계는 없듯이 MVC Pattern 에도 한계가 존재한다. 복잡한 대규모 프로그램의 경우 다수의 View와 Model이 Controller를 통해 연결되기 때문에 컨트롤러가 불필요하게 커지는 현상이 발생하기도 한다. 또한 View를 업데이트하기 위해서는 결국 View와 Model 사이에 의존성이 존재하기 때문에 문제가 발생할 수 있다. 복잡한 화면을 구성하는 경우에도 동일한 현상이 발생하는데 이를 'Massive-View-Controller' 라고 한다. 이러한 단점을 보완하기 위해 다양한 패턴(MVP, MVVM, Redux Pattern)이 파생되었다.

- ### MVP Pattern

![image](https://user-images.githubusercontent.com/66311161/193447302-6063ec91-7765-4bfb-8c69-7845dc43e5b3.png)

MVP Pattern은 기존 MVC Pattern에서 Model과 View의 의존성 문제를 해결하기 위해 파생된 아키텍처 패턴이다. MVP Pattern은 Model, View, Presenter 컴포넌트로 이루어져있다. 

Model과 View는 MVC Pattern과 동일하고, Controller 대신 Presenter가 존재한다. 여기서 Presenter는 View에서 요청한 정보로 Model을 가공해 View에게 전달하는 역할을 하는데 여기서 컨트롤러와 차이점은 Presenter가 View의 인터페이스까지 포함한다는 점이다. Presenter는 사용자로부터 받는 모든 입력값을 수집하며 이것들을 모델에 바로 보내고, 결과를 뷰로 전달한다.

MVP Pattern에서 모든 입력들은 View로 전달된다. Presenter는 입력에 해당하는 Model을 업데이트하고 Model업데이트 결과를 기반으로 View를 업데이트 한다. 이렇게 Presenter가 중간에서 Model과 View 사이에서 관리를 해주기 때문에 둘 사이의 의존성이 없다. 

- ### MVVM Pattern

![image](https://user-images.githubusercontent.com/66311161/193447307-9fc00677-31eb-449a-b661-a8ec919955c4.png)

MVVM Pattern은 MVC Pattern의 Controller 대신 View Model이라는 컴포넌트를 사용한 아키텍처 패턴이다. MVVM Pattern도 마찬가지로 비즈니스 로직과 프레젠테이션 로직을 UI로부터 분리하기 위함이 목표다. 

MVVM Pattern은 Model과 View간의 의존성 뿐만 아니라 Controller와 View 간의 의존성도 고려하여 각 구성요소가 독립적으로 작성되고 테스트될 수 있도록 설계되어있다. View Model이 입력에 해당하는 로직을 처리해서 View에게 데이터를 전달하지만, View Model은 View를 참조하지 않는다. 따라서 View는 자신이 이용할 ViewModel을 선택해 바인딩하여 업데이트를 받는다. 여기서 Command Pattern이나 Data Binding을 사용할 수 있다. 

