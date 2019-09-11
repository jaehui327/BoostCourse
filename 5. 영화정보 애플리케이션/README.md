# 5. 영화정보 애플리케이션

##### 0. Hello!
* [x] 파트개요
* 서버 API 통신
* 영화정보 보여주기
* 왜 이 프로젝트를 할까?
  * 현업의 서비스와 가까워지기
  * 서버와 통신
    - URLSession 활용
    - 비동기 프로그래밍
  - 지난 파트 습득개념 총동원

##### 1. 얼럿과 액션시트
* [x] 1) 얼럿과 액션시트는?
1. 얼럿과 액션시트의 구성요소
- UIAlertController 클래스는 사용자에게 표시할 얼럿 또는 액션시트의 구성에 관한 메서드와 프로퍼티를 포함하고 있습니다.
- UIAlertController 클래스를 통해 얼럿 또는 액션시트를 구성한 후 UIViewController의 `present(_:animated:completion:)`메서드를 사용하여 사용자에게 얼럿 또는 액션시트를 모달로 보여줍니다.
2. 얼럿과 액션시트의 주요 프로퍼티와 주요 메서드
```swift
//얼럿 뷰 컨트롤러의 객체를 초기화합니다.
init(title:message:preferredStyle:)
//얼럿이나 액션시트에 액션을 추가합니다.
func addAction(UIAlertAction)
//얼럿을 통해 텍스트를 입력받고자 하는 경우 텍스트 필드를 추가합니다.
func addTextField(configurationHandler: ((UITextField) -> Void)? = nil)
//사용자가 얼럿 또는 액션시트에 응답하여 실행할 수 있는 액션입니다.
var actions: [UIAlertAction]
//얼럿 컨트롤러의 스타일입니다. 얼럿(alert)과 액션시트(actionSheet)가 있습니다.
var preferredStyle: UIAlertControllerStyle
```
3. 얼럿과 액션시트의 스타일
- default: 액션 버튼의 기본 스타일입니다.
- cancel: 액션 작업을 취소하거나 상태 유지를 위해 변경사항이 없을 경우 적용하는 스타일입니다.
- destructive: 취하게 될 액션이 데이터를 변경되거나 삭제하여 돌이킬 수 없는 상황이 될 수 있음을 나타낼 때 사용하는 스타일입니다.
4. 얼럿과 액션시트가 사용되는 경우
- 얼럿
  - 중요한 액션을 하기 전 경고가 필요한 경우
  - 액션을 취소할 기회를 제공해야 하는 경우
  - 사용자의 작업을 한 번 더 확인하거나 삭제 등의 작업을 수행하거나 문제 사항을 알릴 때
  - 결정이 필요한 중요 정보를 표시할 경우
- 액션시트
  - 사용자가 고를 수 있는 액션 목록이 여러 개일 경우
  - 새 작업 창을 열거나, 종료 여부 확인 시
  - 사용자의 결정을 되돌리거나 그 동작이 중요하지 않을 경우

* [x] 2) 얼럿과 액션시트 보여주기 

##### 2. 탭바 컨트롤러
* [x] 1) 탭바란?
1. 탭바의 구조
- 사용자가 탭바의 항목(Item)을 선택하면 해당 항목에 연결된 뷰 컨트롤러의 콘텐츠가 화면에 보이게 됩니다. 
- 주로 여러 메뉴를 구성할 때 많이 사용합니다. 카테고리 사이의 전환을 위해 사용하거나 다양한 관점으로 같은 정보를 제공하는 데 사용합니다.
- 주로 프레임워크에서 제공하는 탭바 컨트롤러(UITabBarController)를 사용하여 제어합니다. 이렇게 탭바와 탭바 컨트롤러를 사용하여 인터페이스를 구성한 것을 탭바 인터페이스라고 부릅니다.
- 탭바 인터페이스는 탭바 컨트롤러가 생성한 탭바 뷰(View)와 탭바 컨트롤러가 관리하는 콘텐츠 뷰 컨트롤러로 구성되어 있습니다. 
2. 탭바 인터페이스 생성하기
  1. 새로운 탭바 컨트롤러 생성하기
  - 탭바 컨트롤러를 객체 라이브러리로부터 드래그 
  - `Is Initial View Controller` 옵션 선택
  2. 이미 존재하는 뷰 컨트롤러를 탭바 컨트롤러에 연결하기
  - 기존에 있는 뷰 컨트롤러(들)를 선택하고 `Editor` -> `Embed   in` -> `Tab bar controller` 선택
  3. 탭바 컨트롤러에 뷰 컨트롤러 추가하기
  - 뷰 컨트롤러를 객체 라이브러리로부터 드래그
  - 탭바 컨트롤러에서부터 키보드의 `control`키를 누른 상태로 드래그 -> Relation Segue의 `view controllers`. 선택

3. 탭바 아이템
- 탭바 뷰에서 각 탭은 이름과 이미지를 표시할 수 있고 뷰 컨트롤러는 이러한 용도로 tabBar프로퍼티를 관리합니다. 
-  탭바 컨트롤러의 탭바 아이템이 6개 이상인 경우, 5번째 탭에 'More'이라는 아이템이 표시되고 사용자가 More 버튼을 누르면 나머지 탭 항목을 선택할 수 있는 인터페이스가 표시됩니다.
- 탭바 델리게이트 `UITabBarControllerDelegate`
  - 사용자가 탭바 인터페이스와 상호작용할 때, 탭바 컨트롤러 객체는 이 상호작용에 관한 알림(notification)을 델리게이트 인스턴스로 보냅니다. 
  - 사용자가 탭을 선택하지 못하게 하거나, 탭을 선택한 후 추가 작업을 수행하거나, 탭 관련 사항을 모니터링하고 사용자화 하기 위해서 델리게이트를 활용해보세요. 
4. 탭바 컨트롤러의 뷰
-UITabBarController 클래스에는 탭바를 구성하고 각 탭에 해당하는 뷰 컨트롤러들을 관리하기 위한 메서드와 프로퍼티가 정의되어 있습니다.
```swift
//탭바 컨트롤러가 관리하는 뷰 컨트롤러의 배열입니다. 즉, 각각의 탭바 항목에 해당하는 뷰 컨트롤러의 목록입니다.
var viewControllers: [UIViewController]?
//탭바 컨트롤러가 관리할 뷰 컨트롤러들을 설정합니다.
func setViewControllers([UIViewController]?, animated: Bool)
//현재 선택된 탭 항목의 인덱스(index)입니다.
var selectedIndex: Int
```

* [x] 2) 탭 인터페이스 구현해보기

##### 3. 네트워킹
* [x] 1) URLSession과 URLSessionDataTask
- HTTP/HTTPS를 통해 콘텐츠(데이터)를 주고받기 위해 API를 제공하는 클래스인 URLSession과 세션 작업을 하나로 나타내는 클래스인 URLSessionTask에 대해 알아봅시다.
1. URLSession과 URLSessionDataTask
- URLSession
  - URLSession은 HTTP/HTTPS를 통해 콘텐츠(데이터)를 주고받는 API를 제공하는 클래스입니다.
  - 이 API는 인증 지원을 위한 많은 델리게이트 메서드를 제공하며, 애플리케이션이 실행 중이지 않거나 일시 중단된 동안 백그라운드 작업을 통해 콘텐츠를 다운로드하는 것을 수행하기도 합니다. 
  - 예를 들면 웹 브라우저를 사용 중인 경우 탭 당 하나의 세션을 만들 수 있습니다. 각 세션 내에서 애플리케이션은 작업을 추가하고, 각 작업은 특정 URL에 대한 요청을 나타냅니다.
  - Request : 서버로 요청을 보낼 때 어떤 (HTTP)메서드를 사용할 것인지, 캐싱 정책은 어떻게 할 것인지 등의 설정을 할 수 있습니다.
  - Response : URL 요청의 응답을 나타내는 객체입니다.
2. 세션
  1. 기본 세션 (Default Session) : 기본 세션은 URL 다운로드를 위한 다른 파운데이션 메서드와 유사하게 동작합니다. 디스크에 저장하는 방식입니다.
  2. 임시 세션 (Ephemeral Session) : 기본 세션과 유사하지만, 디스크에 어떤 데이터도 저장하지 않고, 메모리에 올려 세션과 연결합니다. 따라서 애플리케이션이 세션을 만료시키면 세션과 관련한 데이터가 사라집니다.
  3. 백그라운드 세션 (Background Session) : 백그라운드 세션은 별도의 프로세스가 모든 데이터 전송을 처리한다는 점을 제외하고는 기본 세션과 유사합니다.
- 세션 만들기
```swift
//init(configuration:) : 지정된 세션 구성으로 세션을 만듭니다.
init(configuration: URLSessionConfiguration)
//shared : 싱글턴 세션 객체를 반환합니다.
class var shared: URLSession { get }
```
- 세션 구성
```swift
//configuration : 이 세션에 대한 구성 객체입니다.
@NSCopying var configuration: URLSessionConfiguration { get }
//delegate : 이 세션의 델리게이트 입니다.
var delegate: URLSessionDelegate? { get }
```
3. 작업(태스크) 상태 제어
- URLSessionTask는 세션 작업 하나를 나타내는 추상 클래스입니다. 하나의 세션 내에서 URLSession 클래스는 세 가지 작업 유형, 즉 데이터 작업(Data Task), 업로드 작업(Upload Task), 다운로드 작업(Download Task)을 지원합니다.
  1. URLSessionDataTask : HTTP의 각종 메서드를 이용해 서버로부터 응답 데이터를 받아서 Data 객체를 가져오는 작업을 수행합니다.
```swift
//dataTask(with:) : URL에 데이터를 요청하는 데이터 작업 객체를 만듭니다.
func dataTask(with url: URL) -> URLSessionDataTask
//dataTask(with:) : URLRequest 객체를 기반으로 URL에 데이터를 요청하는 데이터 작업 객체를 만듭니다.
func dataTask(with request: URLRequest) -> URLSessionDataTask
```
  2. URLSessionUploadTask : 애플리케이션에서 웹 서버로 Data 객체 또는 파일 데이터를 업로드하는 작업을 수행합니다. 주로 HTTP의 POST 혹은 PUT 메서드를 이용합니다.
```swift
//uploadTask(with:from:) : URLRequest 객체를 기반으로 URL에 데이터를 업로드하는 작업을 만듭니다.
func uploadTask(with request: URLRequest, from bodyData: Data) -> URLSessionUploadTask
//uploadTask(with:fromFile:) : URLRequest 객체를 기반으로 URL에 파일을 업로드하는 업로드 작업을 만듭니다.
func uploadTask(with request: URLRequest, fromFile fileURL: URL) -> URLSessionUploadTask
```
  3. URLSessionDownloadTask : 서버로부터 데이터를 다운로드 받아서 파일의 형태로 저장하는 작업을 수행합니다. 애플리케이션의 상태가 대기 중이거나 실행 중이 아니라면 백그라운드 상태에서도 다운로드가 가능합니다.
```swift
//downloadTask(with:) : URL에 요청한 데이터를 다운로드 받아서 파일에 저장하는 다운로드 작업을 만듭니다.
func downloadTask(with url: URL) -> URLSessionDownloadTask
//downloadTask(with:) : URLRequest 객체를 기반으로 URL에 요청한 데이터를 다운로드 받아서 파일로 저장하는 다운로드 작업을 만듭니다.
func downloadTask(with request: URLRequest) -> URLSessionDownloadTask
```
- 데이터 작업은 서버로부터 어떤 응답이라도 Data 객체의 형태로 전달받을 때 사용하며, 업로드 작업 및 다운로드 작업은 단순한 바이너리 파일의 전달에 목적을 둔다고 볼 수 있습니다.
- JSON, XML, HTML 데이터 등 단순한 데이터의 전송에는 주로 데이터 작업을 사용하며, 용량이 큰 파일의 경우 애플리케이션이 백그라운드 상태인 경우에도 전달할 수 있도록 업로드(다운로드) 작업을 주로 사용합니다.
- 작업(태스크) 상태 제어
```swift
//cancel() :  작업을 취소합니다.
func cancel()
//resume() : 일시중단된 경우 작업을 다시 시작합니다.
 func resume()
//suspend() : 작업을 일시적으로 중단합니다.
func suspend()
//state : 작업의 상태를 나타냅니다.
var state: URLSessionTask.State { get }
//priority : 작업처리 우선순위입니다. 0.0부터 1.0 사이입니다.
var priority: Float { get set }
```

* [x] 2) App Transport Security
1. ATS란?
- ATS는 애플리케이션과 웹 서비스 사이에 통신 시 보안 향상을 위한 기능으로 iOS 9.0, macOS 10.11부터 적용 가능합니다. 
- 모든 인터넷 통신 시 안전한 프로토콜을 사용하도록 보장하는 것으로 사용자의 민감한 정보가 유출되는 것을 방지합니다.
- 등장 배경 
  - 다양한 종류의 애플리케이션이 개인의 여러 가지 정보(연락처, 사진, 건강정보, 메시지, 메일 등)를 다루게 되면서 사용자 정보보호에 대한 중요성이 한층 부각되었습니다.
  - 그런데 기존의 보안/암호 기술은 오래되어 공격에 취약해졌지만, 컴퓨터 성능은 점점 발전하면서 새롭게 등장하는 네트워크 공격이 강력해지자 이에 대응하기 위해 2015년 ATS를 도입하게 되었습니다.
  - 2016년부터 새롭게 만들어지는 애플리케이션은 반드시 ATS를 사용해야 하며, 기존에 개발된 애플리케이션은 ATS를 사용할 수 있도록 네트워크 보안을 강화해야 합니다.
2. ATS의 동작과 용어
- ATS 동작
  - URLSession, CFURL 그리고 NSURLConnection API를 이용해 데이터를 주고받을 때 ATS 기능을 기본적으로 사용하게 됩니다.
  - ATS가 활성화되어있을 때는 HTTP 통신을 할 수 없으며 애플에서 권장하는 아래 요구 사항을 충족하지 않은 네트워크는 연결에 실패할 수 있습니다.
    - 서버는 TLS(Transport Layer Security) 프로토콜 버전 1.2 이상을 지원해야 합니다.
    - 적어도 2048비트 이상의 RSA 키 또는 256비트 이상의 ECC(Elliptic-Curve) 키가 있는 SHA256을 인증서에 사용해야 합니다.
    - 암호 연결은 아래 허용된 암호 목록으로 제한합니다.
      - TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384
      - TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256
      - TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384
      - TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA
      - TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256
      - TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA
      - TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384
      - TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256
      - TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384
      - TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256
      - TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA
- 용어 정리
  - 전송 계층 보안 (Transport Layer Security - TLS) : 암호 프로토콜입니다. 서버와 클라이언트 애플리케이션이 네트워크로 통신하는 과정에서 도청, 간섭, 위조를 방지하기 위해서 설계되었습니다.
  - HTTPS (Hypertext Transfer Protocol Secure) : TLS를 사용해 암호화된 연결을 하는 HTTP(Hypertext Transfer Protocol)를 HTTPS라고 합니다.
- TLS는 다양한 종류의 보안 통신을 하려는 프로토콜이고, HTTPS는 TLS 위에 HTTP 프로토콜을 얹어 보안된 HTTP 통신을 하는 프토로콜입니다.
3. ATS 기능의 예외사항과 비활성화 방법
- 예외 사항
  - AVFoundation 프레임워크를 통한 스트리밍 서비스
  - WebKit을 통한 콘텐츠 요청
  - 로컬 네트워크 연결
  - 그 외에는 서버가 최신 TLS 버전으로 업그레이드할 때까지 애플리케이션의 유지 보수를 위해 일시적으로 ATS 기능을 사용하지 않는 것이 가능하며, App Store 심사 시 정당한 이유를 설명하는 문서가 필요할 수도 있습니다.
- ATS 기능 비활성화 방법 : 해당 프로젝트의 info.plist 파일에서 설정합니다.
  - 모든 HTTP 통신 허용 : `App Transport Security Settings`-> `Allow Arbitrary Loads` -> `YES`
  - ATS에서 제외할 특정 도메인 지정 : `App Transport Security Settings`-> `Exception Domains` -> `특정 도메인` -> `NSTemporaryExceptionAllowsInsecureHTTPLoads` -> `YES`
* [x] 3) 서버에 데이터 요청하기

##### 4. GCD
* [x] 1) Grand Central Dispatch란?
1. Grand Central Dispatch(GCD)란?
- Grand Central Dispatch(GCD)는 멀티코어와 멀티 프로세싱 환경에서 최적화된 프로그래밍을 할 수 있도록 애플이 개발한 기술입니다. 
- . 기본적으로 스레드 풀의 관리를 프로그래머가 아닌 운영체제에서 관리하기 때문에 프로그래머가 태스크(작업)을 비동기적으로 쉽게 사용할 수 있습니다. 
- 프로그래머가 실행할 태스크(작업)을 생성하고 Dispatch Queue에 추가하면 GCD는 태스크(작업)에 맞는 스레드를 자동으로 생성해서 실행하고 작업이 종료되면 해당 스레드를 제거합니다.
2. 디스패치 대기열
- 디스패치 대기열(Dispatch Queue)은 작업을 연속적 혹은 동시에 진행하기는 하지만, 언제나 먼저 들어오면 먼저 나가는 순서로 실행됩니다.
- Serial Dispatch Queue는 한 번에 하나의 작업만을 실행하며, 해당 작업이 대기열에서 제외되고 새로운 작업이 시작되기 전까지 기다립니다.
- 이와는 반대로 Concurrent Dispatch Queue는 이미 시작된 작업이 완료될 때까지 기다리지 않고 가능한 많은 작업을 진행합니다. 
3. 디스패치 소스
- 디스패치 소스(Dispatch Source)는 특정 유형의 시스템 이벤트를 비동기적으로 처리하기 위한 C 기반 메커니즘입니다. 
- 특정 유형의 시스템 이벤트에 대해 정보를 캡슐화하고, 해당 이벤트가 발생할 때마다 특정 클로저(블록) 객체 혹은 기능을 디스패치 대기열(Dispatch Queue)에 전달합니다. 
4. 연산 대기열
- 연산 대기열(Operation Queue)은 Concurrent Dispatch Queue와 동일하게 동작하며, Operation Queue 클래스에 의해 구현됩니다. 
- 디스패치 대기열은 항상 먼저 들어오면 먼저 나가는 순서(FIFO - First in First out)로 작업을 실행하지만, 연산 대기열(Operation Queue)은 작업의 실행 순서를 결정할 때에 다른 요인들을 고려합니다.
- 연산 대기열(Operation Queue)은 디스패치 대기열(Dispatch Queue)과 매우 유사한 클래스입니다.
5. GCD와 연산 대기열 (Operation Queue)의 차이점
  1. Operation Queue에서는 동시에 실행할 수 있는 연산(Operation)의 최대 수를 지정할 수 있습니다.
  2. Operation Queue에서는 KVO(Key Value Observing)을 사용할 수 있는 많은 프로퍼티들이 있습니다.
  3. Operation Queue에서는 연산(Operation)을 일시 중지, 다시 시작 및 취소를 할 수 있습니다.
- Operation Queue : 비동기적으로 실행되어야 하는 작업을 객체 지향적인 방법으로 사용하는 데 적합합니다. KVO(key Value Observing)를 사용해 작업 진행 상황을 감시하는 방법이 필요할 때도 적합합니다.
- GCD : 작업이 복잡하지 않고 간단하게 처리하거나 특정 유형의 시스템 이벤트를 비동기적으로 처리할 때 적합합니다. 예를 들면 타이머, 프로세스 등의 관련 이벤트입니다.
* [x] 2) DispatchQueue
1. 대기열(Queue) 유형
- DispatchQueue는 작업항목의 실행을 관리하는 클래스입니다.
- 기열(Queue)에 추가된 작업항목은 시스템이 관리하는 스레드 풀에서 처리하고 작업을 완료하면 스레드를 알아서 해제합니다. 
- DispatchQueue의 장점은 일반 스레드 코드보다 쉽고 효율적으로 코드를 작성할 수 있다는 점입니다. 
- 주로 iOS에서는 서버에서 데이터를 내려받는다든지 이미지, 동영상 등 멀티미디어 처리와 같이 CPU 사용량이 많은 처리를 별도의 스레드에서 처리한 뒤 메인 스레드로 결과를 전달하여 화면에 표시합니다. 
- DispatchQueue를 생성 시 기본은 Serial입니다. Concurrent 유형으로 바꾸려면 별도로 명시만 해주면 됩니다.
- Serial : 대기열(Queue)에 등록한 순서대로 작업을 실행합니다. 하나의 작업을 실행하고 실행이 끝날 때까지 대기열(Queue)에 있는 다른 작업을 미루고 있다가 이전 작업이 끝나면 실행합니다.
- Concurrent : 실행 중인 작업이 끝나기를 기다리지 않고 대기열(Queue)에 있는 작업을 동시에 별도의 스레드를 사용하여 실행합니다. 즉, 병렬처리 방식입니다.
2. DispatchQueue 클래스의 주요 메서드와 주요 프로퍼티
```swift
//main : 애플리케이션의 메인 스레드와 연결된 Serial DispatchQueue를 반환.
class var main: DispatchQueue { get }
//sync(execute:) : DispatchQueue에서 실행을 위해 클로저를 대기열(Queue)에 추가하고 해당 클로저가 완료될 때까지 대기합니다.
func sync(execute block: () -> Void)
//async(execute:) : DispatchQueue에서 비동기 실행을 위해 클로저를 추가하고 즉시 실행합니다.
 func async(execute workItem: DispatchWorkItem)
```

* [x] 3) DispatchQueue를 활용한 비동기 프로그래밍

##### 5. 노티피케이션 센터
* [x] 1) 노티피케이션 센터와 노티피케이션
1. 노티피케이션의 주요 프로퍼티
- Notification이란 등록된 노티피케이션에 노티피케이션 센터를 통해 정보를 전달하기 위한 구조체입니다.
```swift
//name : 알림을 식별하는 태그
var name: Notification.Name
//object : 발송자가 옵저버에게 보내려고 하는 객체. 주로 발송자 객체를 전달하는 데 쓰임
var object: Any?
//userInfo : 노티피케이션과 관련된 값 또는 객체의 저장소
var userInfo: [AnyHashable : Any]?
```
- 예) 특정 행동으로 인해 작업이 시작되거나 완료되는 시점에 다른 인스턴스로 노티피케이션이 발생 시 필요한 데이터를 같이 넘겨 줄 수 있습니다. 간단한 예로 네트워킹을 이용하는 애플리케이션이라면 네트워킹이 시작 및 완료되는 시점, 음악 및 동영상 재생 등에도 재생이 끝나는 시점에 관련 정보를 넘겨 줄 수 있습니다.
2. 노티피케이션 센터를 얻는 방법과 옵저버
- NotificationCenter란 등록된 옵저버에게 동시에 노티피케이션을 전달하는 클래스입니다. 
- NotificationCenter 클래스는 노티피케이션을 발송하면 노티피케이션 센터에서 메세지를 전달한 옵저버의 처리할 때까지 대기합니다.
- 즉, 흐름이 동기적(synchronous)으로 흘러갑니다. 
- 노티피케이션을 비동기적으로 사용하려면 NotificationQueue를 사용하면 됩니다.
- 기본 노티피케이션 센터 얻기
```swift
//default : 애플리케이션의 기본 노티피케이션 센터입니다.
 class var `default`: NotificationCenter { get }
```
- 옵저버 추가 및 제거
```swift
//addObserver(forName:object:queue:using:) : 노티피케이션을 노티피케이션 대기열(Queue)과 대기열(Queue)에 추가할 블록(스위프트의 클로저), 노티피케이션 이름을 노티피케이션 센터의 메서드를 가리키는 장소(디스패치 테이블, Dispatch Table)에 이름을 추가합니다. 여기서 object에 특정 객체를 명시하면 명시한 객체가 발송한 노티피케이션일 때에만 해당 이름의 노티피케이션을 수신합니다.
func addObserver(forName name: NSNotification.Name?, object obj: Any?, queue: OperationQueue?, using block: @escaping (Notification) -> Void) -> NSObjectProtocol
//addObserver(_:selector:name:object:) : 노티피케이션을 노티피케이션 센터의 메서드를 가리키는 장소에 이름을 추가합니다.
 func addObserver(_ observer: Any, selector aSelector: Selector, name aName: NSNotification.Name?, object anObject: Any?)
//removeObserver(_:name:object:) : 노티피케이션 센터의 메서드를 가리키는 장소에서 일치하는 이름을 제거합니다.
func removeObserver(_ observer: Any, name aName: NSNotification.Name?, object anObject: Any?)
```
- 노티피케이션 발송
```swift
//post(name:object:userInfo:) : 지정된 이름, 보낸 객체, 보낼 정보로 노티피케이션을 만들어 노티피케이션 센터에 발송합니다.
 func post(name aName: NSNotification.Name, object anObject: Any?, userInfo aUserInfo: [AnyHashable : Any]? = nil)
//post(name:object:) : 지정된 이름, 보낸 객체로 노티피케이션을 만들어 노티피케이션 센터에 발송합니다.
func post(name aName: NSNotification.Name, object anObject: Any?)
```
- 예제
1. 일반 노티피케이션
- 옵저버 등록
```swift
NotificationCenter.default.addObserver(self, selector: #selector(didRecieveTestNotification(_:)), name: NSNotification.Name("TestNotification"), object: nil)

@objc func didRecieveTestNotification(_ notification: Notification) {
         print("Test Notification")
}
```
- 발송자
```swift
NotificationCenter.default.post(name: NSNotification.Name("TestNotification"), object: nil, userInfo: nil)
```
2. User Info 정보를 담은 노티피케이션
- 옵저버 등록
```swift
NotificationCenter.default.addObserver(self, selector: #selector(didReceiveTestNotification(_:)), name: NSNotification.Name("TestNotification"), object: nil)

@objc func didReceiveTestNotification(_ notification: Notification) {
 		guard let testString: String = notification.userInfo?["TestString"] as? String else { return }
         print("testString :", testString)
 }
```
- 발송자
```swift
let userInfo: [AnyHashable: Any] = ["TestString":"Hi"]

NotificationCenter.default.post(name: NSNotification.Name("TestNotification"), object: nil, userInfo: userInfo)
```

* [x] 2) 노티피케이션 센터의 활용

##### 6. Summary
* [x] 1) 돌아보기

