# 1. 음원 재생기 애플리케이션

###### 0.Hello!

- [x] **파트 개요**

  목표 : 

  1. iOS 프로그래밍 환경 익히기
  2. 차후 프로젝트의 복습용 보조교재

  **1차시는 따라하기 형식으로 진행

###### 1.시작 그리고 Xcode

- [x] **1) Xcode 설치 및 프로젝트 생성**
- [x] **2) Xcode 톺아보기**

###### 2. 애플리케이션 만들기

- [x] **1) 프로젝트에 이미지 추가하기**

- 에셋 카탈로그(Asset Catalog)

  : 애플리케이션에 사용될 다양한 에셋

- 앱 슬라이싱(App Slicing)

  : 애플리케이션이 디바이스에 설치될 때 앱 스토어와 운영체제가 그 디바이스의 특성에 맞게 설치하도록 하는 설치 최적화 기술

- 앱 시닝(App Thinning) 

  : 개발자가 애플리케이션의 전체 버전을 iTunes Connect에 업로드하게 되면, 애플리케이션이 지원하는 다양한 디바이스에 대한 여러 조각의 애플리케이션 번들(app bundle)을 생성하고 디바이스에 알맞은 조각을 전달하는 기술

- ###### `command` + `shift` + `o` : 파일 빠르게 찾기

- [x] **2) 인터페이스 빌더로 화면 구성하기**

- [x] **3) 인터페이스 빌더의 객체를 코드와 연결(IBOutlet)**

- 객체 이름 변경 시 오류 방지법 (앱 강제 종료 시 의심해보기)
  1. 오른쪽 마우스 클릭 -> Refactor -> Rename
  2. 수동으로 잘못된 연결 삭제

- [x] **4) 인터페이스 빌더의 객체를 코드와 연결(IBAction)**


- [x] **5) UIButton, UISlider, UILabel**

  1. ##### **UIButton** 

- 버튼의 상태

  `default`, `highlighted`, `focused`, `selected`, `disabled`


- [x] **6) 구현 코드 작성하기**
```swift
//MARK - Properties
//코드가 길어졌을 때 찾기 유용합니다.
```
1. ##### **AUFoundation**

: 다양한 Apple 플랫폼에서 사운드 및 영상 미디어의 처리, 제어, 가져오기 및 내보내기 등 광범위한 기능을 제공하는 프레임워크



###### 3. Foundation과 UIKit 그리고 Cocoa Touch

- [x] **1) Cocoa Touch 프레임워크란?**

- [x] **2) UIKit이란?**

- [x] **3) Foundation이란?**

  : 원시 데이터 타입(String, Int, Double), 컬렉션 타입(Array, Dictionary, Set) 및 운영체제 서비스를 사용해 애플리케이션의 기본적인 기능을 관리하는 프레임워크



###### 4. 오토 레이아웃

- [x] **1) 오토 레이아웃이란?**

  : 가장 편리하게 사이즈에 구애받지 않고 시각적으로 동일한 화면을 구현할 수 있는 방법

  : 뷰의 제약 사항을 바탕으로 뷰 체계 내의 모든 뷰의 크기와 위치를 동적으로 계산합니다. 


  - 안전 영역(Safe Area)

    - 상태바, 내비게이션바, 툴바, 탭바를 가리는 것을 방지하는 영역입니다.
    - 기존의 상/하단 레이아웃 가이드(Top/Bottom Layout Guide)를 대체하며, 하위 버전에도 호환하여 작동합니다.

    ```swift
    //안전 영역 레이아웃 가이드 접근 
    var safeAreaLayoutGuide: UILayoutGuide
    ```

  - 앵커(Anchor)

    - 사용 예제
      1. 중앙에 버튼을 배치하고 버튼의 top anchor를 사용하여 레이블을 버튼의 상단으로부터 10만큼 떨어지도록 배치하기
      2. 속성에 곱해지는 multiplier를 활용해보기

    ```swift
    import UIKit
    
    class ViewController: UIViewController {
        @IBOutlet weak var button: UIButton!
        @IBOutlet weak var label: UILabel!
        
        override func viewDidLoad(){
            super.viewDidLoad()
            
            //오토레이아웃이 도입되기 전 뷰를 유연하게 표현할 수 있도록 오토리사이징 마스크를 사용하였습니다.
            //기존의 오토리사징 마스크가 가지고 있던 제약조건이 자동으로 추가되기 때문에 충돌하게 될 가능성을 배제합니다.
            //인터페이스 빌더에서 오토레이아웃을 적용한 경우에는 자동으로 값이 false로 설정됩니다.
            button.translatesAutoresizingMaskIntoConstraints = false
            //버튼을 중앙에 배치하기 위해 수평과 수직의 중앙 앵커를 뷰의 중앙에 기준을 잡습니다.
            var constraintX: NSLayoutConstraint
            constraintX = button.centerXAnchor.constraint(equalTo: self.view.centerXAnchor)
            var constraintY: NSLayoutConstraint
            constraintY = button.centerYAnchor.constraint(equalTo: self.view.centerYAnchor)
            
            //생성된 제약을 적용합니다.
            constraintX.isActive = true
            constraintY.isActive = true
            
            label.translatesAutoresizingMaskIntoConstraints = false
            //레이블의 수평 중앙을 버튼의 수평 중앙 앵커를 기준으로 제약을 생성합니다.
            var buttonConstraintX: NSLayoutConstraint
            buttonConstraintX = label.centerXAnchor.constraint(equalTo: button.centerXAnchor)
            //레이블의 하단 앵커를 버튼의 상단 앵커로부터 10만큼의 거리를 두도록 합니다.
            //상단 앵커기준으로 위로의 거리는 부호가 - 라는 점을 주목하세요.
            var topConstraint: NSLayoutConstraint
            topConstraint = label.bottomAnchor.constraint(equalTo: button.topAnchor, constant: -10)
            
            //생성된 제약을 적용하기 위해 isActive 프로퍼티를 true로 설정해줍니다.
            buttonConstraintX.isActive = true
            topConstraint.isActive = true
            
            //label이 button 너비의 두배가 되도록 설정합니다.
            var widthConstraint: NSLayoutConstraint
    		widthConstraint = label.widthAnchor.constraint(equalTo: 		button.widthAnchor, multiplier: 2.0)
    
    		//실제 너비를 확인하기 위해서 배경색상을 지정해봅니다.
    		label.backgroundColor = UIColor.brown
    		button.backgroundColor = UIColor.blue
            
            widthConstraint.isActive = true
        }
    }
    ```

- [x] **2) 오토 레이아웃 구현하기(코드)**

  * NSLayoutConstraint

    * 오토레이아웃 방정식

    **view1.attr1 = view2.attr2 \* multiplier + constant** **item.attribute = toItem.attribute \* multiplier + constant

  * Visual Format Language

    | 기호 및 문자열 | 설명                          |
    | -------------- | ----------------------------- |
    | \|             | superView 입니다.             |
    | -              | 표준 간격입니다.              |
    | ==             | 같은 너비입니다.              |
    | -10-           | 사이의 간격이 10포인트입니다. |
    | <=50           | 50보다 작거나 같습니다.       |
    | >=50           | 50보다 크거나 같습니다.       |
    | @750           | 우선도를 지정할 수 있습니다.  |
    | H              | 수평 방향입니다. (가로)       |
    | V              | 수직 방향입니다. (세로)       |

  * **Tip**: 오토레이아웃에서는 뷰에 제약을 적용할 때, 어떤 제약을 우선시해야 하는지를 우선도로 결정합니다. 만약, **하나의 속성(attribute)에 적용할 수 있는 두 개 이상의 제약이 있다면 그중 우선도가 높은 제약이 적용됩니다.** 우선도는 **1부터 1000까지**의 정수로 표현할 수 있습니다.

  예제 1. flexibleButton의 **너비 값이 70포인트보다 크거나 같고 100포인트보다 작거나 같도록 제약**을 생성합니다. (Multiple Predicates)

  ```swift
   NSLayoutConstraint(item: flexibleButton,
   			  attribute: .width,
   			  relatedBy: .greaterThanOrEqual,
   			  toItem: nil,
   			  attribute: .notAnAttribute,
   			  multiplier: 1.0,
   			  constant: 70.0)
   			  
   NSLayoutConstraint(item: flexibleButton,
   			  attribute: .width,
   			  relatedBy: .lessThanOrEqual,
   			  toItem: nil,
   			  attribute: .notAnAttribute,
   			  multiplier: 1.0,
   			  constant: 100.0)
  //or
   H:[flexibleButton(>=70,<=100)]
  ```

  예제 2. **button1, button2, textField와 superView의 간격은 표준 간격**(8포인트)이며 **textField의 너비 값은 20포인트보다 크거나 같도록** 제약을 생성합니다. (A Complete Line of Layout)

  ```swift
   // button1
   NSLayoutConstraint(item: button1,
   			  attribute: .left,
   			  relatedBy: .equal,
   			  toItem: self.view,
   			  attribute: .left,
   			  multiplier: 1.0,
   			  constant: 8.0)
   			  
   // button2
   NSLayoutConstraint(item: button2,
   			  attribute: .left,
   			  relatedBy: .equal,
   			  toItem: button1,
   			  attribute: .right,
   			  multiplier: 1.0,
   			  constant: 8.0)
   			  
   // textField
   NSLayoutConstraint(item: textField,
   			  attribute: .left,
   			  relatedBy: .equal,
   			  toItem: button2,
   			  attribute: .right,
   			  multiplier: 1.0,
   			  constant: 8.0)
   
   NSLayoutConstraint(item: textField,
   			  attribute: .width,
   			  relatedBy: .greaterThanOrEqual,
   			  toItem: nil,
   			  attribute: .notAnAttribute,
   			  multiplier: 1.0,
   			  constant: 20.0)
   
   NSLayoutConstraint(item: textField,
   			  attribute: .right,
   			  relatedBy: .equal,
   			  toItem: self.view,
   			  attribute: .right,
   			  multiplier: 1.0,
   			  constant: -8.0)
  //or
   H:|-[find]-[findNext]-[findField(>=20)]-|
  ```

- [x] **3) 오토 레이아웃 구현하기(인터페이스 빌더)**

  

###### 5. iOS의 View 체계

- [x] **1) iOS의 View 체계**

- 뷰 계층의 생성과 관리

  1. 코드 작성 방식

  * 서브뷰를 부모뷰에 추가하기 위해, 부모뷰의` addSubView(_:)` 메서드를 호출합니다. -> 이 메서드는 해당 서브뷰를 서브뷰 목록의 마지막에 추가합니다.

  * 목록의 중간에 삽입하기 위해서는  `insertSubview(_:at:)`

  * 부모뷰 내에 이미존재하는 서브뷰를 정렬하기 위해서는 `bringSubView(toFront:)`, `sendSubview(toBack:)`

    1. 서브뷰 생성하기

    ```swift
    import UIKit
    class ViewController: UIViewController {
        override func viewDidLoad() {
            super.viewDidLoad()
            //서브뷰 생성
            let frame = CGRect(x: 60, width: 240, height: 120)
            let subView = UIView(frame: frame)
            //서브뷰의 색상
            subView.backgroundColor = UIColor.green //서브뷰의 색상
            //서브뷰 추가하기
            view.addSubview(subView)
        }
    }
    ```

    2. 서브뷰 제거하기

    ```swift
    subView.removeFromSuperview()
    ```

  2. 인터페이스 빌더 방식

  * 나중에 추가된 또는 서브뷰 배열의 끝으로 옮겨진 서브뷰가 맨 위에 보여지게 됩니다.

- CGRect

  : 뷰의 프레임(frame)과 바운드(bounds)는 [CGRect](https://developer.apple.com/documentation/coregraphics/cgrect)라는 구조체를 통해서 표현됩니다. 

  `CGRect(x: CGFloat, y: CGFloat, width: CGFloat, height: CGFloat)`

  * origin프로퍼티는 CGPoint 타입으로 사각형의 시작점을 나타냅니다. 

    `CGPoint(x: CGFloat, y:CGFloat)`

  * size프로퍼티는 CGSize타입으로 사각형의 높이와 너비를 나타냅니다.

    `CGSize(width: CGFloat, height: CGFloat)`

  

###### 6. MVC

- [x] **1) 프로그래밍 디자인 패턴이란?**

: 소프트웨어를 설계할 때 특정 상황에서 자주 사용하는 패턴을 정형화한 것이며, 

좋은 소프트웨어 설계를 위한 개발자들의 경험적 산물이라고 할 수 있습니다. 

* 디자인 패턴의 종류

  • **싱글턴 패턴 (Singleton Pattern)**

  객체의 생성에 관련된 패턴으로서 특정 클래스의 인스턴스가 오직 하나임을 보장하고 이 인스턴스에 접근할 방법을 제공합니다.

  • **퍼사드 패턴 (Facade Pattern)**

  시스템의 복잡성을 줄이기 위해 서브 시스템을 구조화하고 서브 시스템으로의 접근을 하나의 퍼사드 객체로 제공하는 패턴입니다.

  • **옵저버 패턴 (Observer Pattern)** : 관찰자

  변화가 있을 때마다 메서드 등을 통해 객체가 직접 목록의 각 옵저버에게 통지하도록 하는 패턴입니다.

*약물의 오남용이 우리 몸에 치명적인 영향을 미칠 수 있듯이 제대로 알지 못하고 사용하는 디자인패턴은 코드에 치명적 영향을 미칠 수 있음을 항상 명심해야 할 것입니다.*

* [x] **2) Model-View-Controller**

  : 애플리케이션의 객체를 **모델, 뷰, 컨트롤러**의 세 가지 역할 중 하나의 역할로 할당합니다.

* **모델** **객체** **(Model Objects)**

  : 애플리케이션과 관련된 데이터를 캡슐화하고, 해당 데이터를 조작하고 처리하는 로직과 계산을 정의합니다. 

* **뷰** **객체** **(View Objects)**

  :  애플리케이션 내에서 사용자가 볼 수 있는 객체를 말합니다.

* **컨트롤러** **객체** **(Controller Objects)**

  : 하나 이상의 애플리케이션 뷰 객체와 하나 이상의 모델 객체 사이의 코디네이터 또는 중개자 역할을 합니다. (ex. 뷰 컨트롤러)

* [x] **3) 직접 찾아보기**

  

###### 7. Apple Developder Documentation

- [x] **1) 애플 개발자 문서 읽기**

  문서 읽기 팁 : 가이드 -> 참조 자료 -> 샘플 코드(프로퍼티, 메서드 숙지)

###### 8. Summary

- [x] **1) 돌아보기**