## 음료 자판기 앱

### step-1

#### 요구사항

- 기존 VendingMachine 프로젝트의 Main, InputView, OutputView를 제외하고 전체 클래스를 프로젝트로 복사한다.
- MVC의 Model과 ViewController 사이 관계에 집중한다.
- ViewController 클래스에 VendingMachine 객체를 변수로 추가하고 viewDidLoad() 함수에서 음료수 객체 3종류를 추가하고 재고 목록을 print() 한다.
- iOS 앱을 구성하는 핵심 객체들과 iOS 메인 런루프 동작 이해하기 위해서 [애플 앱 프로그래밍 가이드](https://developer.apple.com/library/content/documentation/iPhone/Conceptual/iPhoneOSProgrammingGuide/Introduction/Introduction.html#//apple_ref/doc/uid/TP40007072)문서를 학습한다.

#### 해결

- iOS 앱을 구성하는 핵심 객체들

  - UIApplication object

    ~~~
    이벤트 루프 및 기타 상위 수준 응용 프로그램 동작을 관리한다. 또한 주요 앱 전환과 푸시 알림과 같은 특수 이벤트를 커스텀 객체인 위임자에게 보고한다. 서브 클래싱 없이 사용할 수 있다.
    ~~~

  - App delegate object

    ~~~
    커스텀 코드의 핵심이다. 이 객체는 UIApplication 객체와 함께 작동하여 응용 프로그램 초기화, 상태 전환 및 많은 고급 응용 프로그램 이벤트를 처리한다. 이 객체는 모든 응용 프로그램에 존재할 수 있는 유일한 객체이기 때문에 응용 프로그램의 초기 데이터 구조를 설정하는 데 자주 사용한다.
    ~~~

  - Documents and data model objects

    ~~~
    데이터 모델 객체는 앱의 콘텐츠를 저장하며 앱에만 적용됩니다. 예를 들어 금융 앱은 금융 거래가 포함된 데이터베이스를 저장할 수 있지만, 페인팅 앱은 해당 이미지를 만들 수 있는 이미지 객체 또는 그리기 명령 시퀀스를 저장할 수 있다. (후자의 경우 이미지 객체는 이미지 데이터의 컨테이너이기 때문에 여전히 데이터 객체다.) 

    응용 프로그램들은 문서 객체(UIDocument의 사용자 정의 하위 클래스)를 사용하여 데이터 모델 객체 일부 또는 전체를 관리 할 수 있다. 문서 객체는 필수는 아니지만 단일 파일 또는 파일 패키지에 속한 데이터를 그룹화하는 편리한 방법을 제공한다. 
    ~~~

  - View controller objects

    ~~~
    뷰 컨트롤러 객체는 화면에 나타나는 앱 컨텐츠 프리젠테이션을 관리한다. 뷰 컨트롤러는 단일 뷰와 하위 뷰의 집합을 관리한다. 화면에 보여질 때, 뷰 컨트롤러는 앱의 윈도우에 설치하여 볼 수 있게 한다. UIViewController 클래스는 모든 뷰 컨트롤러 객체의 기본 클래스이다. 뷰 로드, 프리젠테이션, 디바이스 회전에 따른 뷰 회전, 그리고 몇 가지 다른 표준 시스템 동작을 위한 기본 기능을 제공한다.

    UIKit및 기타 프레임 워크는 이미지 피커, 탭 바 인터페이스, 그리고 네이게이션 인터페이스와 같은 표준 시스템 인터페이스를 구현하기 위한 추가 뷰 컨트롤러를 정의한다.
    ~~~

  - UIWindow object

    ~~~
    UIWindow 객체는 화면에서 하나 이상의 뷰 프리젠테이션을 조정한다. 대부분의 앱에는 메인 화면에 콘텐츠를 제공하는 오직 하나의 윈도우를 갖고있지만, 외부 디스플레이에 표시된 콘텐츠에 대한 추가 윈도우가 있을 수 있다. 앱의 콘텐츠를 변경하려면, 뷰 컨트롤러를 사용하여 해당 윈도우에 표시된 뷰를 변경한다. 윈도우 자체를 대체할 수는 없다.
    ~~~

  - View objects, control objects, and layer objects

    ```
    뷰 및 컨트롤은 앱 콘텐츠의 시각적 표현을 제공한다. 뷰는 지정된 직사각형 영역에 내용을 그리고 그 영역 내의 이벤트에 응답하는 객체이다. 컨트롤은 버튼, 텍스트 필드 및 토글 스위치와 같은 익숙한 인터페이스 개체를 구현하는 특수 유형의 뷰다.
    UIKit 프레임워크는 다양한 유형의 컨텐츠를 표시하기 위한 표준 뷰를 제공한다. 또한 UIView (또는 그 자손)를 직접 서브 클래싱하여 고유한 사용자 정의 뷰를 정의 할 수 있다.
    뷰와 컨트롤을 통합하는 것 외에도 앱은 Core Animation 레이어를 뷰와 컨트롤 계층에 통합 할 수 있다. 레이어 객체는 실제로 시각적인 컨텐츠를 나타내는 데이터 객체다. 뷰는 레이어 객체를 집중적으로 사용하여 컨텐츠를 렌더링한다. 인터페이스에 사용자 정의 레이어 객체를 추가하여 복잡한 애니메이션 및 기타 유형의 정교한 시각 효과를 구현할 수도 있다.
    ```

- iOS 메인 런 루프 동작

  ~~~
  앱의 메인 런 루프는 모든 사용자 관련 이벤트를 처리한다. UIApplication 객체는 실행 시 기본 실행 루프를 설정하고 이를 사용하여 이벤트를 처리하고 뷰 기반 인터페이스에 대한 업데이트를 처리한다. 이름에서 알 수 있듯이 기본 실행 루프는 앱의 주 스레드에서 실행된다. 이 동작은 사용자 관련 이벤트가 수신된 순서대로 순차적으로 처리되도록 한다.
   사용자가 기기와 상호 작용할 때 시스템에서 이러한 상호 작용과 관련된 이벤트를 생성하고 UIKit에 의해 설정된 특수 포트를 통해 앱에 전달돤다. 이벤트는 앱에 의해 내부적으로 대기열에 넣어지고 실행을 위해 메인 런 루프에 하나씩 전달된다. UIApplication 객체는 이벤트를 수신하여 수행해야 할 작업을 결정하는 첫 번째 객체다. 터치 이벤트는 대개 메인 윈도우 객체에 전달되고, 터치는 터치가 발생한 뷰에 디스패치 한다. 다른 이벤트는 다양한 앱 객체를 통해 약간 다른 경로를 취할 수 있다.
  ~~~

### step-2

- ~12/4

#### 실행화면

![Alt text](VendingMachineApp/image/vendingMachineScreenshot.jpeg)

