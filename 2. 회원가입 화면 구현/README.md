# 2. 회원가입 화면 구현

#부스트코스 #iOS프로그래밍

###### 0.Hello!

- [x] **파트 개요**

###### 1. Human Interface Guidelines

- [x] **1) H.I.G 란?**

: 애플리케이션을 개발할 때 필요한 디자인과 동작을 포함한 여러 규칙을 통하여 사용자 인터페이스를 어떻게 구성하는 방법에 대한 지침을 제시합니다. 

###### 2. 화면의 전환

- [x] **1) 내비게이션 인터페이스란?**

- 내비게이션 스택의 푸시(push)

  UIViewController 인스턴스가 생성되고 내비게이션 스택에 추가됩니다.

- 내비게이션 스택의 팝(pop)

  UIViewController의 인스턴스는 다른 곳에서 참조되고 있지 않다면 메모리에서 해제되고, 내비게이션 스택에서 삭제됩니다.

- 내비게싱션 인터페이스 구성하기

  1. 스토리보드

     [Editor] - [Embed In] - [Navigation Controller]

  2. 코드

     ex) 내비게이션 컨트롤러가 애플리케이션 윈도우(window)의 루트 뷰로서 역할을 한다면, 내비게이션 컨트롤러를 `applicationDidFinishLaunching:` 메서드에 구현할 수 있습니다.

     ```swift
     func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool {
             // Override point for customization after application launch.
             
             // 루트 뷰 컨트롤러가 될 뷰 컨트롤러를 생성합니다.
             let rootViewController = UIViewController()
             // 위에서 생성한 뷰 컨트롤러로 내비게이션 컨트롤러를 생성합니다.
             let navigationController = UINavigationController(rootViewController: rootViewController)
             
             self.window = UIWindow(frame: UIScreen.main.bounds)
             // 윈도우의 루트 뷰 컨트롤러로 내비게이션 컨트롤러를 설정합니다.
             self.window?.rootViewController = navigationController
             self.window?.makeKeyAndVisible()
             
             return true
         }
     ```

- [x] **2) 내비게이션 인터페이스 구현해보기**
- 코드로 pop 액션 작성

```swift
 @IBAction func popToPrev() {
     self.navigationController?.popViewController(animated: true)
    }
```

- [x] **3) 모달이란?**

: **이목을 집중해야 하는** 화면을 다른 화면 위로 띄워(Presenting) 표현하는 방식입니다.

- 뷰 컨트롤러를 화면상에 나타내는 방법(Presenting)

  1. 컨테이너뷰 컨트롤러에 임베드
  2. 프레젠테이션을 통해서 나타내기

- 다른 스토리보드에서 정의된 뷰 컨트롤러 나타내기

  ```swift
  let storyboard: UIStoryboard = UIStoryboard(name: "SecondStoryboard", bundle: nil)
  if let myViewController: MyViewController = storyboard.instantiateViewController(withIdentifier: "MyViewController") as? MyViewController {
  	// 뷰 컨트롤러를 구성 합니다.
  	
  	// 뷰 컨트롤러를 나타냅니다.
  	self.present(myViewController, animated: true, completion: nil)
  }
  ```

- [x] **4) 모달 구현해보기**

- 내비게이션: 흐름 vs 모달: 간단한 정보

###### 3. 뷰의 상태변화 감지

- [x] **1) 뷰의 상태변화 감지 매서드**

- 상태 변화 메서드

  ```swift
  //메모리에 로드된 직후 호출되는 메서드
  func viewDidLoad()
  //뷰 계층에 추가되고 표시되기 직전에 호출되는 메서드
  func viewWillAppear(_  animated: Bool)
  //화면이 표시되면 호출되는 메서드
  func viewDidAppear(_ animated: Bool)  
  //사라지기 직전에 호출되는 메서드
  func viewWillDisappear(_ animated: Bool) 
  //뷰 게층에서 사라진 후 호출되는 메서드
  func viewDidDisappear(_ animated: Bool)
  ```

- 레이아웃 변화 메서드

  ```swift
  //서브뷰의 레이아웃을 변경하기 직전에 호출되는 메서드
  func viewWillLayoutSubviews()
  //서브뷰의 레이아웃이 변경된 후 호출되는 메서드
  func viewDidLayoutSubviews()
  ```

- [x] **2) 직접 확인해보기**

###### 4. Delegation

- [x] **1) Delegation?**

```
Delegate: [명사] 대표(자), 사절, 위임, 대리(자)
		  [동사] (권한, 업무 등을) 위임하다, (대표를) 선정하다
```

* **델리게이션 디자인 패턴(Delegation Design Pattern)**

  : **사용자 인터페이스 제어**에 관련된 권한을 위임받아서,

  하나의 객체가 다른 객체를 대신해 동작 또는 조정할 수 있는 기능을 제공합니다.

  : 특정 상황에 대리자에게 메시지를 전달하고 그에 적절한 응답 받기 위한 목적으로 사용됩니다.

* **데이터소스(DataSource)**

  : **데이터를 제어하는 기능**을 위임받습니다.

* **프로토콜(Protocol)** 

  : 코코아터치에서 프로토콜을 사용해 델리게이션과 데이터소스를 구현할 수 있습니다.

  : 객체간 소통을 위한 강력한 통신 규약으로 데이터나 메시지를 전달할 때 사용합니다.

* [x] **2) Delegation 디자인 패턴의 활용**

###### 5. Singleton

- [x] **1) Singleton?**

: 특정 클래스의 인스턴스가 오직 하나임을 보장하는 객체

: 애플리케이션 내에서 특정 클래스의 인스턴스가 딱 하나만 있기 때문에 다른 인스턴스들이 공유해서 사용할 수 있습니다.

: 객체가 불필요하게 여러 개 만들어질 필요가 없는 경우에 많이 사용합니다. (ex. 환경설정, 네트워크 연결처리, 데이터 관리 등)

- [x] **2) Singleton 구현해보기**

- StackView

  수평 또는 수직 방향의 선형적인 레이아웃의 인터페이스를 사용할 수 있도록 해줍니다.   

  `arrangedSubviews` 프로퍼티에 스택뷰에 포함된 뷰들을 관리합니다.    

###### 6. Target-Action

- [x] **1) Target-Action 디자인 패턴이란?**

Target-Action 디자인 패턴에서 객체는 이벤트가 발생할 때 다른 객체에 메시지를 보내는 데 필요한 정보를 포함합니다.    

메서드가 여러 클래스에 정의되어 있는 경우도 있고, 그런 클래스의 인스턴스가 여러개인 상황에 사용합니다.

```swift
// 프로그래밍 방식
@objc func doSomething(_ sender: Any) {
}
// 인터페이스 빌더
@IBAction func doSomething(_ sender: Any) { 
}
```

* 컨트롤 이벤트

UIKit에는 `UIButton`, `UISwitch`, `UIStepper` 등 `UIControl`을 상속받은 다양한 컨트롤 클래스가 있습니다.

컨트롤 객체에 발생한 다양한 이벤트 종류를 특정 액션 메서드에 연결할 수 있습니다. 

- [x] **2) Target-Action 디자인 패턴의 활용**

- UIDatePicker

  - 인터페이스 빌더

  1.  ViewController에서 코드 작성

  ```swift
  @IBAction func didDatePickerValueChanged(_ sender: UIDatePicker){
          print("value change")
  }
  ```

  2. 인터페이스 빌더에서 action: value changed 로 연결
  * 코드

  ```swift
  @IBAction func didDatePickerValueChanged(_ sender: UIDatePicker){
          print("value change")
  }
  override func viewDidLoad() {
         self.datePicker.addTarget(self, action: #selector(didDatePickerValueChanged(_:)), for: UIControlEvents.valueChanged)
      }
  ```

- DateFormatter

날짜와 텍스트 표현 간의 변환을 할 수 있게 해줍니다. 

특정 요구 사항에 따라 date formatter의 `dateStyle`(날짜)과 `timeStyle`(시간)프로퍼티를 설정합니다. 

```swift
//DateFormatter property
let dateFormatter: DateFormatter = {
        let formatter: DateFormatter = DateFormatter()
//        formatter.dateStyle = .medium
//        formatter.timeStyle = .medium
        formatter.dateFormat = "yyyy/MM/dd hh:mm:ss"
        return formatter
    }()

@IBAction func didDatePickerValueChanged(_ sender: UIDatePicker){
        let date: Date = sender.date
        let dateString: String = self.dateFormatter.string(from: date)
        self.dateLabel.text = dateString
    }
```

###### 7. Gesture Recognizer

- [x] **1) Gesture Recognizer란?**
- Gesture Recognizer

특정 제스처 이벤트가 일어날 때 마다 각 타깃에 맞는 액션 메시지를 보내어 제스처 관련 이벤트를 처리할 수 있습니다.

```swift
@IBAction func myActionMethod()
@IBAction func myActionMethod(_ sender: UIGestureRecognizer)
```

* 인터페이스 빌더에서 제스처 인식기 추가

  1. 객체 라이브러리에서 Tap Gesture Recognizer를 뷰로 드래그 앤 드롭 합니다.
  2. 스토리보드의 Tap Gesture Recognizer를 컨트롤 + 드래그하여 ViewController로 타깃-액션을 연결합니다.

* 코드 작성을 통해 제스처 인식기 추가하기

  ```swift
  override func view DidLoad() {
  	super.viewDidLoad()
      //액션 타깃을 통한 제스처 인식기 초기화 및 생성
  	let tapRecognizer = UITapGestureRecognizer(target: self, 	action: #selector(tapView(gestureRecognizer:)))
  	//뷰에 제스처 인식기 연결하기
  	self.view.addGestureRecognizer(tapRecognizer)
  }
  //액션 메서드
  @objc func tapView(gestureRecognizer: UIGestureRecognizer) {
      print("Tapped")
  }
  ```

* [x] **2) Gesture Recognizer의 사용**

###### 8. Summary

- [x] **1) 돌아보기**
