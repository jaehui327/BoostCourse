# 4. 내 사진 관리 애플리케이션  
#부스트코스 #iOS프로
###### 0. Hello!
* [x] 파트 개요
* Photos Framework
* 사진앨범 구현하기  

* 왜 이 프로젝트를 할까?
  * 컬렉션뷰 학습
  * 비동기 프로그래밍
    * Operation
    * Operation Queue
  * UI 컴포넌트
    * 스크롤 뷰
    * 내비게이션 아이템

###### 1. Photos
* [x] 1) Photos 프레임워크
* Photos 프레임워크는 iOS 및 macOS에서 사진 애플리케이션, 사진 확장 기능을 지원하는 클래스를 제공합니다. 
* 모델 클래스의 인스턴스 : 에셋(이미지, 비디오, 라이브 포토), 에셋 컬렉션(앨범, 특별한 순간), 컬렉션 리스트(앨범 폴더, 특별한 순간)
1. 객체 가져오기 및 변경 요청
  * 읽기 전용이며, 변경할 수 없습니다.
  * 메타 데이터만 포함합니다.
  - 해당 객체를 사용하여 데이터를 가져와서 작업할 수 있습니다. 변경시엔 변경 요청 객체를 만들고 공유 PHPhotoLibrary 객체에 명시적으로 알려줍니다.  
2. Photos 애플리케이션의 기능들을 지원
  - PHCollectionList 클래스를 사용해 Photos 애플리케이션의 특별한 순간 계층에 해당하는 에셋을 찾습니다.
  - 버스트, 파노라마 사진 및 고프레임 비디오를 식별하려면 PHAsset 클래스를 사용하세요. 
3. 에셋과 미리보기 로딩 및 캐싱
  PHImageManager 클래스를 사용해 지정된 크기로 에셋의 이미지를 요청하거나 비디오 에셋에 사용할 AVFoundation 객체를 요청합니다.
4. 에셋 콘텐츠 편집

  - PHAsset 및 PHAssetChangeRequest 클래스는 편집을 위해 사진 또는 비디오를 요청하여 사진 라이브러리에 편집한 내용을 반영하는 메서드를 정의합니다.  
* `PHPhotoLibrary` : 사용자의 사진 라이브러리에 대한 접근 및 변경을 관리하는 공유 객체입니다.
* 에셋 검색과 조사 : 사진 라이브러리의 콘텐츠를 나타냅니다. 읽기 전용이며 변경 불가하고 메타 데이터만 포함합니다.
  * PHAsset, PHAssetCollection, PHCollectionList, PHCollection, PHObject, PHFetchResult, PHFetchOptions
* 에셋 콘텐츠 로딩 : 이미지, 비디오, 라이브 포토 콘텐츠를 요청할 수 있습니다.
  * PHImageManager, PHCachingImageManager, PHImageRequestOptions, PHVideoRequestOptions, PHLivePhtoRequestOptions, PHLivePhoto
* 변경 요청 : 에셋이나 컬렉션을 변경하려면 변경 요청 객체를 만들고 명시적으로 사진 라이브러리에 반영합니다.
  * PHAssetChangeRequest, PHAssetCollectionChangeRequest, PHCollectionListCHangeRequest
* 에셋 콘텐츠 수정 : 애플리케이션 또는 확장 프로그램에서 사진 라이브러리의 편집 및 반영을 위해 에셋 데이터에 접근합니다.
  * PHContentEditingInput, PHContentEditingOutput, PHAdjustmentData, PHContentEditingInputReuestOptions, PHLivePhotoEditingContext, PHLivePhtoFrame
* 변경사항 관찰 : 다른 애플리케이션이나 다른 기기에서 사진의 정보를 변경할 때 마다 애플리케이션에 알려줍니다.
  * PHPhotoLibraryChangeObserver, PHChange, PHObjectChangeDetails, PHFetchResultChangeDetails
* 에셋 리소스로 작업하기 : 에셋 리소스 객체는 각 에셋의 데이터 저장소를 나타냅니다. 이러한 객체를 사용해 에셋을 직접 백업하고 복원할 수 있습니다.
  * PHAssetResource, PHAssetCreationRequest, PHAssetResouceCreationOptions, PHAssetResouceManger, PHAssetResouceRequestOption

* [x] 2) 사진첩에서 사진 가져오기 
* [x] 3) 사진첩에서 사진 삭제하기

###### 2. 동시성(Concurrency) 프로그래밍
* [x] 1) 동시성 프로그래밍과 비동기 프로그래밍
1. 프로세서, 코어, 프로그램과 프로세스, 스레드
- 프로세서 : 하드웨어적인 측면에서 컴퓨터 내에서 프로그램을 수행하는 하드웨어 유닛입니다. 대표적으로 중앙처리장치(Central Processing Unit - CPU)가 이에 속합니다. 
- 코어 : 프로세서에서 코어는 주요 연산회로입니다. 
- 프로그램(Program)과 프로세스(Process)
  - 프로그램 : 일반적으로 보조기억 장치에 저장된 실행코드 즉, 생명이 없는 상태를 말합니다.
  - 프로세스는 프로그램을 구동하여 프로그램 자체와 프로그램의 상태가 메모리상에서 실행되는 작업 단위를 말합니다. 프로세스 관리는 운영체제에서 담당합니다.
- 스레드(Thread) : 하나의 프로세스 내에서 실행되는 작업흐름의 단위를 말합니다. 
2. 비동기 프로그래밍과 동시성 프로그래밍
- 비동기(Asynchronous) 프로그래밍 : 프로그램의 주 실행 흐름을 멈추어서 기다리는 부분 없이 바로 다음 작업을 실행할 수 있게 하는 방식입니다. 즉, 코드의 실행 결과 처리를 별도의 공간에 맡겨둔 뒤 결과를 기다리지 않고 바로 다음 코드를 실행하는 병렬처리 방식입니다. 
- 동시성(Concurrency) 프로그래밍 : 논리적인 용어로 동시에 실행되는 것처럼 보이는 것입니다. 싱글 코어(멀티 코어에서도 가능)에서 멀티스레드를 동작시키기 위한 방식으로 멀티 태스킹을 위해 여러 개의 스레드가 번갈아 가면서 실행되는 방식입니다. 
3. 병렬성 프로그래밍
- 병렬성(Parallelism) 프로그래밍 : 물리적으로 동시에 정확히 동시에 실행되는 것을 말합니다. 멀티 코어에서 멀티 스레드를 동작시키는 방식으로 데이터 병렬성(Data Parallelism)과 작업 병렬성(Task Parallelism)으로 구분됩니다.
  - 데이터 병렬성 : 전체 데이터를 나누어 서브 데이터들로 만든 뒤, 서브 데이터들을 병렬 처리해서 작업을 빠르게 수행하는 방법입니다.
  - 작업 병렬성 : 서로 다른 작업을 병렬 처리하는 것을 말합니다.
4. 동시성과 병렬성의 차이
- 동시성(Concurrecny) : 통장을 만들러 온 N개의 대기열과 한 명 이상의 은행직원
- 병렬성(Parallelism) : 통장을 만들러 온 N개의 대기열과 N명의 은행직원
**즉, 동시성은 싱글코어 및 멀티코어에서 모두 구현할 수 있지만, 병렬성은 멀티 코어에서만 구현할 수 있습니다.**

5. iOS 환경 동시성 프로그래밍 지원 종류
- Grand Central Dispatch (GCD) : 멀티 코어와 멀티 프로세싱 환경에서 최적화된 프로그래밍을 할 수 있도록 애플이 개발한 기술입니다.
- 연산 대기열 (Operation Queue) : 비동기적으로 실행되어야 하는 작업을 객체 지향적인 방법으로 사용합니다.
- Thread : 멀티스레드 프로그래밍을 위한 애플에서 제공하는 스레드 클래스입니다.

* [x] 2) OperationQueue
1. 연산객체(Operation Object)
- Operation은 태스크(작업)와 관련된 코드와 데이터를 나타내는 추상 클래스입니다. 연산(Operation)은 작업이 끝날 때까지 대기열에 남아 있습니다. 연산(Operation)을 대기열에서 제거하는 방법은 연산(Operation)을 취소하는 방법뿐입니다. 
- Operation Queue는 연산(Operation)의 실행을 관리합니다. 대기열(Queue)에 추가한 동작은 직접 제거할 수 없습니다. 
- 취소하는 방법은 연산 객체(Operation Object)의 cancel()메서드를 호출하거나 Oeration Queue의 cancelAllOperations() 메서드를 호출하여 대기열에 있는 모든 연산(Operation)을 취소하는 방법이 있습니다. 
- 실행 중인 연산(Operation)의 경우 연산 객체(Operation Object)의 취소 상태를 확인하고 실행 중인 연산(Operation)을 중지하고 완료 상태로 변경됩니다.
- 연산 객체 (Operation Object)는 애플리케이션에서 수행하려는 연산(Operation)을 캡슐화하는 데 사용하는 Foundation 프레임 워크의 Operation 클래스 인스턴스입니다.
2. 대기열과 연산의 관리
- 특정 Operation Queues 가져오기
```swift
//current : 현재 작업을 시작한 Operation Queue를 반환합니다.
class var current: OperationQueue? { get }
//main : 메인 스레드와 연결된 Operation Queue를 반환합니다.
class var main: OperationQueue { get }
```
- 대기열(Queue)에서 동작(Operation) 관리
```swift
//addOperation(_:) : 연산 객체(Operation Object)를 대기열(Queue)에 추가합니다.
 func addOperation(_ op: Operation)
//addOperations(_:waitUntilFinished:) : 연산 객체(Operation Object) 배열을 대기열(Queue)에 추가합니다.
func addOperations(_ ops: [Operation], waitUntilFinished wait: Bool)
//addOperation(_:) : 전달한 클로저를 연산 객체(Operation Object)에 감싸서 대기열(Queue)에 추가합니다.
func addOperation(_ block: @escaping () -> Void)
//cancelAllOperations() : 대기 중이거나 실행 중인 모든 연산(Operation)을 취소합니다.
func cancelAllOperations()
//waitUntilAllOperationsAreFinished() : 대기 중인 모든 연산(Operation)과 실행 중인 연산(Operation)이 모두 완료될 때까지 현재 스레드로의 접근을 차단합니다.
 func waitUntilAllOperationsAreFinished()
```
- 연산(Operation) 실행 관리
```swift
//maxConcurrentOperationCount : 동시에 실행할 수 있는 연산(Operation)의 최대 수입니다.
 var maxConcurrentOperationCount: Int { get set }
//qualityOfService : 대기열 작업을 효율적으로 수행할 수 있도록 여러 우선순위 옵션을 제공합니다.
var qualityOfService: QualityOfService { get set }
```
- 연산(Operation) 중단
```swift
//isSuspended : 대기열(Queue)의 연산(Operation) 여부를 나타내기 위한 부울 값입니다. false인 경우 대기열(Queue)에 있는 연산(Operation)을 실행하고, true인 경우 대기열(Queue)에 대기 중인 연산(Operation)을 실행하진 않지만 이미 실행 중인 연산(Operation)은 계속 실행됩니다.
var isSuspended: Bool { get set }
```
- 대기열(Queue)의 구성
```swift
//name : Operation Queue의 이름
var name: String? { get set }​
```

* [x] 3) OperationQueue를 활용하여 비동기 프로그래밍 해보기 

###### 3. 스크롤뷰
* [x] 1) 스크롤뷰란?
1. 스크롤뷰란?
- 스크롤뷰는 스크롤뷰 안에 포함된 뷰를 상,하,좌,우로 스크롤 할 수 있고 확대 및 축소할 수 있는 뷰입니다. 
- 그리고 스크롤뷰를 상속받아 활용되는 뷰로는 UITableView, UICollectionView, UITextView등 여러 UIKit 클래스가 있습니다.
2. 스크롤뷰의 주요 메서드와 프로퍼티
   1. 스크롤뷰 상호작용 : `UIScrollViewDelegate`
   2. 콘텐츠 크기 및 오프셋 관리
```swift
//setContentOffset(_:animated:) : 스크롤뷰의 원점에 대한 콘텐츠뷰의 오프셋 설정.
func setContentOffset(_ contentOffset: CGPoint, animated: Bool)
```
   3. 콘텐츠 삽입 동작 관리
   4. 스크롤뷰 구성
```swift
//isScrollEnabled : 스크롤링이 사용 가능한지 아닌지를 결정하는 부울 값
var isScrollEnabled: Bool { get set }
//isDirectionalLockEnabled : 스크롤이 특정 방향으로 고정할지를 결정하는 부울 값
 var isDirectionalLockEnabled: Bool { get set }
//bounces : 스크롤뷰가 가장자리를 통과해서 다시 튀어나오는지 제어하는 부울 값
 var bounces: Bool { get set }
```
   5. 스크롤링 상태 가져오기
```swift
//isTracking : 사용자가 스크롤을 시작하기 위해 콘텐츠를 터치한 여부를 반환
 var isTracking: Bool { get }
//isDragging : 사용자가 콘텐츠를 스크롤하고 있는지 나타내는 부울 값
var isDragging: Bool { get }
```
   6. 스크롤 인디케이터 및 새로고침 제어 관리
   7. 특정 위치로 스크롤 하기
```swift
//scrollRectToVisible(_:animated:) : 콘텐츠의 특정 위치로 스크롤 하여 화면에 표시
func scrollRectToVisible(_ rect: CGRect,  animated: Bool)
```
   8. 확대 및 축소
```swift
//zoomScale : 스크롤뷰 콘텐츠에 적용되는 현재 배율
var zoomScale: CGFloat { get set }
//maximumZoomScale :  스크롤뷰 콘텐츠에 적용되는 최대 배율
 var maximumZoomScale: CGFloat { get set }
//isZoomBouncing : 확대 및 축소가 지정한 배율 제한을 초과했음을 나타내는 부울 값
 var isZoomBouncing: Bool { get }
//zoom(to:animated:) : 콘텐츠 특정 영역 확대
 func zoom(to rect: CGRect, animated: Bool)
```
   9. 키보드 관리
   10. UIScrollViewDelegate 프로토콜
```swift
//scrollViewDidScroll(_:) : 콘텐츠뷰를 스크롤 할 때 델리게이트에 알림
optional func scrollViewDidScroll(_ scrollView: UIScrollView)
//scrollViewDidEndDecelerating(_:) : 스크롤링 동작이 감속이 끝났을 때 델리게이트에 알림
optional func scrollViewDidEndDecelerating(_ scrollView: UIScrollView)
//viewForZooming(in:) : 스크롤뷰에서 확대 및 축소를 할 때 확대 및 축소를 할 뷰 인스턴스를 요청
optional func viewForZooming(in scrollView: UIScrollView) -> UIView?
```

* [x] 2) 스크롤뷰로 이미지 확대하기

###### 4. 내비게이션 아이템
* [x] 1) 내비게이션 아이템이란?
1. 내비게이션 아이템
* 내비게이션바의 콘텐츠를 표시하는 객체입니다. 
* 뷰 컨트롤러가 전환될 때마다 내비게이션바는 하나의 공동 객체지만, 내비게이션 아이템은 각각의 뷰 컨트롤러가 가지고 있는 프로퍼티입니다. 
*  내비게이션바가 내비게이션 컨트롤러와 연관이 있다면 내비게이션 아이템은 해당 뷰 컨트롤러와 연관이 있습니다. 
2. 내비게이션 아이템의 주요 프로퍼티와 주요 메서드
```swift
//title : 내비게이션바에 표시되는 내비게이션 아이템의 제목. 기본값은 nil입니다.
var title: String? { get set }
//setHidesBackButton(_:animated:) : 뒤로 버튼이 숨겨져 있는지를 설정하고, 전환 애니메이션 효과 적용
func setHidesBackButton(_ hidesBackButton: Bool, animated: Bool)
```
3. 내비게이션 아이템 커스터마이징
- 내비게이션 아이템은 크게 좌, 우 바 버튼 아이템과 중앙 타이틀 영역이 있습니다. 좌측 바 버튼, 우측 바 버튼 아이템의 경우 타입은 UIBarButtonItem 입니다. 
```swift
//leftBarButtonItems : 좌측 아이템 영역의 UIBarButtonItem의 바 버튼 아이템 배열
 var leftBarButtonItems: [UIBarButtonItem]? { get set }
//setLeftBarButtonItems(_:animated:) : 좌측 아이템 영역에 UIBarButtonItem 타입의 객체들을 순차적으로 설정하고 애니메이션 효과를 적용
 func setLeftBarButtonItems(_ items: [UIBarButtonItem]?, animated: Bool)
```

* [x] 2) 바 버튼 아이템이란?
1. 바 버튼 아이템의 스타일
- UIToolbar 또는 UINavigationBar (backBarButtonItem,leftBarButtonItem,rightBarButtonItem등)에 배치할 수 있는 특수한 버튼입니다. 
- Tip : iOS 11에서는 UIBarButtonItem을 오토레이아웃 제약 없이 내비게이션 아이템으로 추가하면 바 버튼 아이템의 프레임이 예상치 못한 크기로 나올 수 있습니다. 이럴 땐 UIBarButtonItem 객체에 적절한 오토레이아웃 제약을 추가한 후 내비게이션 아이템으로 설정하면 설정한 제약에 따라 알맞은 크기로 볼 수 있습니다.
2. 바 버튼 아이템의 주요 프로퍼티와 주요 메서드
```swift
//style : 아이템의 스타일.
//done, add, edit, cancel, save, reply, action, trash, bookmarks, search, refresh, stop, camera, play, pause, fastForward, rewind
var style: UIBarButtonItemStyle { get set }
```

* [x] 3) 바 버튼 아이템 얹어보기

###### 5. 컬렉션뷰
* [x] 1) 컬렉션뷰란?
1. 컬렉션뷰
- 유연하고 변경 가능한 레이아웃을 사용하여 데이터 아이템의 정렬된 세트를 표시하는 수단입니다. 
2. 컬렉션뷰의 구성요소
- 셀(Cell) : 컬렉션뷰의 주요 콘텐츠를 표시합니다. 컬렉션뷰는 컬렉션뷰 데이터 소스 객체에서 표시할 셀에 대한 정보를 가져옵니다. 각 셀은 UICollectionViewCell 클래스의 인스턴스 또는 UICollectionViewCell을 상속받은 클래스의 인스턴스입니다.
- 보충 뷰(Supplementary views) : 섹션에 대한 정보를 표시합니다. 셀과 달리 보충 뷰는 필수는 아니며, 사용법과 배치 방식은 사용되는 레이아웃 객체가 제어합니다. 헤더와 푸터를 예로 들 수 있습니다.
- 데코레이션 뷰(Decoration views) : 콘텐츠가 스크롤 되는 컬렉션뷰에 대한 배경을 꾸밀 때 사용합니다. 레이아웃 객체는 데코레이션 뷰를 사용하여 커스텀 배경 모양을 구현할 수 있습니다.
- 레이아웃 객체(Layout Object) : 레이아웃 객체는 컬렉션뷰 내의 아이템 배치 및 시각적 스타일을 결정합니다. 컬렉션뷰 데이터 소스 객체가 뷰와 표시할 콘텐츠를 제공한다면, 레이아웃 객체는 크기, 위치 및 해당 뷰의 레이아웃과 관련된 특성들을 결정합니다.
3. 컬렉션뷰 구현을 이루기 위한 클래스 및 프로토콜
- UICollectionView : 사용자에게 보여질 컬렉션 형태의 뷰입니다. 
- UICollectionViewCell : UICollectionView 인스턴스에 제공되는 데이터를 화면에 표시하는 역할을 담당합니다.
- UICollectionReusableView : 뷰 재사용 메커니즘을 지원합니다.
- UICollectionViewFlowLayout : 컬렉션뷰를 위한 디폴트 클래스로, 그리드 스타일로 셀들을 배치하도록 설계되어있습니다. scrollDirection 프로퍼티를 통해 수평 및 수직 스크롤을 지원합니다.
- UICollectionViewLayoutAttributes : 컬렉션뷰 내의 지정된 아이템의 레이아웃 관련 속성을 관리합니다.
- UICollectionViewDataSource 프로토콜 : 컬렉션뷰에 필요한 데이터 및 뷰를 제공하기 위한 기능을 정의한 프로토콜입니다.
- UICollectionViewDelegate 프로토콜 : 컬렉션뷰에서 아이템의 선택 및 강조 표시를 관리하고 해당 아이템에 대한 작업을 수행할 수 있는 기능을 정의한 프로토콜입니다.
- UICollectionViewDelegateFlowLayout 프로토콜 : UICollectionViewLayout 객체와 함께 그리드 기반 레이아웃을 구현하기 위한 기능을 정의한 프로토콜입니다.

* [x] 2) 컬렉션뷰 셀
1. 컬렉션뷰 셀
- 컬렉션뷰의 셀은 냉장고 속에 있는 반찬통으로 생각할 수 있습니다. 컬렉션뷰라는 냉장고가 있고, 냉장고 안에는 실제 반찬(콘텐츠)을 담고 있는 컬렉션뷰 셀이라는 반찬통이 있다고 생각할 수 있습니다.
  - 컬렉션뷰 셀은 데이터 아이템을 화면에 표시합니다.
  - 하나의 셀은 하나의 데이터 아이템을 화면에 표시합니다.
  - 컬렉션뷰 셀은 뷰의 재사용 메커니즘을 지원합니다.
2. UICollectionViewCell 클래스
```swift
//셀이 선택되었는지를 나타냅니다. 셀이 선택되어있지 않다면 이 프로퍼티의 값은 false입니다.
var isSelected: Bool 
//셀의 드래그 상태가 변경되면 호출됩니다.
func dragStateDidChange(_:)
```
3. 컬렉션뷰 셀과 테이블뷰 셀 비교
- 테이블뷰 셀의 구조는 콘텐츠 영역과 액세서리뷰 영역으로 나뉘었지만, 컬렉션뷰 셀은 배경뷰와 실제 콘텐츠를 나타내는 콘텐츠뷰로 나뉘었습니다.
- 테이블뷰 셀은 기본으로 제공되는 특정 스타일을 적용할 수 있지만 컬렉션뷰 셀은 특정한 스타일이 따로 없습니다.
- 테이블뷰 셀은 목록형태로만 레이아웃 되지만, 컬렉션뷰 셀은 다양한 레이아웃을 지원합니다.

* [x] 3) DataSource와 Delegate?
1. 컬렉션뷰 데이터소스
- 컬렉션뷰 데이터소스 객체는 컬렉션뷰와 관련하여 가장 중요한 객체이며, 필수로 제공해야 합니다.
- 컬렉션뷰의 콘텐츠(데이터)를 관리하고 해당 콘텐츠를 표현하는 데 필요한 뷰를 만듭니다.
- 데이터소스 객체는 최소한 `collectionView(_:numberOfItemsInSection:)`과 `collectionView(_:cellForItemAt:)` 메서드를 구현해야 하며 나머지 메서드는 선택사항입니다.
```swift
//지정된 섹션에 표시할 항목의 개수를 묻는 메서드.
func collectionView(_ collectionView: UICollectionView, numberOfItemsInSection section: Int) -> Int
//컬렉션뷰의 지정된 위치에 표시할 셀을 요청하는 메서드.
func collectionView(_ collectionView: UICollectionView, cellForItemAt indexPath: IndexPath) -> UICollectionViewCell
//컬렉션뷰의 섹션의 개수를 묻는 메서드. 이 메서드를 구현하지 않으면 섹션 개수 기본 값은 1.
optional func numberOfSections(in collectionView: UICollectionView) -> Int
//지정된 위치의 항목을 다른 위치로 이동하도록 지시하는 메서드.
optional func collectionView(_ collectionView: UICollectionView, moveItemAt sourceIndexPath: IndexPath, to destinationIndexPath: IndexPath)
```
2. 컬렉션뷰 델리게이트
- 컬렉션뷰 델리게이트 프로토콜은 컬렉션뷰에서 셀의 선택 및 강조표시를 관리하고 해당 셀에 대한 작업을 수행할 수 있는 메서드를 정의합니다. 이 프로토콜의 메서드는 모두 선택사항입니다.
```swift
//collectionView(_:didSelectItemAt:) : 지정된 셀이 선택되었음을 알리는 메서드.
optional func collectionView(_ collectionView: UICollectionView, didSelectItemAt indexPath: IndexPath)
```

* [x] 4) 간단한 컬렉션뷰 만들기
* [x] 5) 컬렉션뷰에 동적으로 데이터 추가하기
* [x] 6) 셀 커스터마이징
* [x] 7) UICollectionViewFlowLayout
1. 플로우 레이아웃 스크롤
- UICollectionViewFlowLayout 클래스를 사용하면 컬렉션뷰의 셀을 원하는 형태로 정렬할 수 있습니다. 플로우 레이아웃은 레이아웃 객체가 셀을 선형 경로에 배치하고 최대한 이 행을 따라 많은 셀을 채우는것을 의미합니다. 
- 수직 스크롤, 수평 스크롤이 있고, 플로우 레이아웃을 사용해 그리드 형태뿐만 아니라 다양한 레이아웃을 구현할 수 있습니다. 예를 들어 셀을 하나의 행으로 만들어 정렬한 후 간격을 조정할 수도 있습니다.
2. 플로우 레이아웃의 구성 단계
   1. 플로우 레이아웃 객체를 작성해 컬렉션뷰의 레이아웃 객체로 지정합니다.
   2. 셀의 너비와 높이를 구성합니다.
   3. 필요한 경우 셀의 간격을 조절합니다.
   4. 원할 경우 섹션 헤더 혹은 섹션 푸터를 크기를 지정합니다.
   5. 레이아웃의 스크롤 방향을 설정합니다.
3. 플로우 레이아웃 속성을 변경
- 플로우 레이아웃 객체는 콘텐츠의 모양을 구성하기 위해 여러 가지 프로퍼티를 제공합니다. 이 프로퍼티에 적절한 값을 설정하면 모든 셀에 동일한 레이아웃이 적용됩니다. 
- 예를 들면 플로우 레이아웃 객체의 itemSize 프로퍼티를 사용하여 셀의 크기를 설정할 경우 모든 셀의 크기가 동일하게 적용됩니다.
4. 플로우 레이아웃의 셀 크기와 셀 및 행의 간격 지정 방법
- 컬렉션뷰의 모든 셀이 같은 크기인 경우 플로우 레이아웃 객체의 itemSize의 프로퍼티에 적절한 너비와 높이 값을 할당합니다. 
- 각각의 셀마다 다른 크기를 지정하려면 컬렉션뷰 델리게이트에서 collectionView:layout:sizeForItemAtIndexPath: 메서드를 구현해야 합니다. 
- 플로우 레이아웃을 사용하여 같은 행의 셀 사이의 최소 간격과 연속하는 행 사이의 최소 간격을 지정할 수 있습니다. 여기서 명심해야 하는 점은 설정하는 간격은 최소 간격이라는 점입니다. 
5. UICollectionViewDelegateFlowlLayout의 주요 선택 메서드
```swift
//collectionView(_:layout:sizeForItemAt:) -> CGSize : 지정된 셀의 크기를 반환하는 메서드.
optional func collectionView(_ collectionView: UICollectionView, layout collectionViewLayout: UICollectionViewLayout, sizeForItemAt indexPath: IndexPath) -> CGSize
//collectionView(_:layout:insetForSectionAt:) -> UIEdgeInsets : 지정된 섹션의 여백을 반환하는 메서드.
optional func collectionView(_ collectionView: UICollectionView, layout collectionViewLayout: UICollectionViewLayout, insetForSectionAt section: Int) -> UIEdgeInsets
//collectionView(_:layout:referenceSizeForHeaderInSection:) -> CGSize : 지정된 섹션의 헤더뷰의 크기를 반환하는 메서드. 크기를 지정하지 않으면 화면에 보이지 않습니다.
optional func collectionView(_ collectionView: UICollectionView, layout collectionViewLayout: UICollectionViewLayout, referenceSizeForHeaderInSection section: Int) -> CGSize
```

* [x] 8) UICollectionViewFlowLayout을 활용하여 셀 크기 조절해보기

###### 6. 자료 공유하기
* [x] 1) 액티비티 뷰 컨트롤러
1. 액티비티의 아이템과 타입
- UIActivityViewController : 애플리케이션 내에서 특정 아이템을 복사하거나 외부 SNS로 공유하는 내보내기 서비스는 사용자가 아이템을 다양한 방식으로 활용하도록 도와줍니다.
-  iOS 6 이상부터 사용 가능한 UIActivityViewController 클래스는 내보내기 서비스를 손쉽게 사용할 수 있도록 해줍니다.
- 공유 가능한 아이템
  - 문자열(String)
  - URL 링크(String)
  - 이미지(UIImage)
  - UIActivityItemSource 프로토콜을 따르는 커스텀 타입의 인스턴스
2. 액티비티 뷰 컨트롤러 클래스의 주요 메서드와 프로퍼티
```swift
// 읽기 목록에 추가
static let addToReadingList: UIActivityType
// 에어드롭으로 공유하기
static let airDrop: UIActivityType
// 연락처에 지정
static let assignToContact: UIActivityType
// Paste Board에 복사
static let copyToPasteboard: UIActivityType
// 메일 보내기
static let mail: UIActivityType
// 메시지 보내기
static let message: UIActivityType
// iBooks에서 열기
static let openInIBooks: UIActivityType
// 페이스북에 공유하기
static let postToFacebook: UIActivityType
// Flickr에 공유하기
static let postToFlickr: UIActivityType
// Tencent Weibo에 공유하기
static let postToTencentWeibo: UIActivityType
// 트위터에 공유하기
static let postToTwitter: UIActivityType
// Vimeo에 공유하기
static let postToVimeo: UIActivityType
// SinaWeibo에 공유하기
static let postToWeibo: UIActivityType
// 프린트
static let print: UIActivityType
// 카메라 롤에 저장하기
static let saveToCameraRoll: UIActivityType
// PDF 생성(iOS 11 부터 사용가능)
static let markupAsPDF: UIActivityType

// 초기화 메서드로, UIActivityViewController 객체를 반환합니다.
init(activityItems: [Any], applicationActivities: [UIActivity]?)
// activityItems: [Any] 공유하려는 아이템으로 UIActivityItemSource 프로토콜을 준수하는 객체를 배열 형태로 넣어줄 수 있습니다.
// applicationActivities: [UIActivity]? 애플리케이션이 지원하는 커스텀 서비스를 나타내는 UIActivity 객체의 배열로, nil 값이 될 수 있습니다.

// 컨트롤러를 닫은 후 실행할 완료 핸들러입니다.
var completionWithItemsHandler: UIActivityViewControllerCompletionWithItemsHandler?

// UIActivityType 중 사용하지 않을 서비스를 지정합니다.
var excludedActivityTypes: [UIActivityType]?
```
- 샘플 코드
```swift
// 1. UIActivityViewController 초기화, 공유 아이템 지정
let imageToShare: UIImage = UIImage(named: "image.png")
let urlToShare: String = "http://www.edwith.org/boostcourse-ios"
let textToShare: String = "안녕하세요, 부스트 코스입니다."

let activityViewController = UIActivityViewController(activityItems: [imageToShare, urlToShare, textToShare], applicationActivities: nil)
    
// 2. 기본으로 제공되는 서비스 중 사용하지 않을 UIActivityType 제거(선택 사항)
activityViewController.excludedActivityTypes = [UIActivityType.addToReadingList, UIActivityType.assignToContact]

// 3. 컨트롤러를 닫은 후 실행할 완료 핸들러 지정
activityViewController.completionWithItemsHandler = { (activity, success, items, error) in
    if success {
	// 성공했을 때 작업
   }  else  {
	// 실패했을 때 작업
   }
}
// 4. 컨트롤러 나타내기(iPad에서는 팝 오버로, iPhone과 iPod에서는 모달로 나타냅니다.)
self.present(activityViewController, animated: true, completion: nil)
```
###### 7. Summary
* [x] 1) 돌아보기
