# 3. 기상정보 애플리케이션
#부스트코스 #iOS프로그래밍
###### 0. Hello!
* [x] **파트 개요**
* JSON 데이터를 활용하여 날씨 정보를 보여줄 수 있는 애플리케이션 제작
  필요한 개념 : `UITableView`, `Navigation Interface`, `Delegation Pattern`, `JSONDecoder`

###### 1. 테이블뷰
* [x] **1) 테이블뷰란?**
* 테이블뷰 
  * 하나의 열(column)과 여러 줄의 행(row)을 지니며, 수직으로만 스크롤 가능합니다.
  * 각 행은 하나의 셀(cell)에 대응합니다.
  * 섹션(section)을 이용해 시각적으로 나눌 수 있습니다.
  * 헤더(header)와 푸터(footer)에 이미지나 텍스트를 추가해 추가 정보를 보여줄 수 있습니다.
* 테이블 뷰 생성
  새로운 테이블뷰를 생성할 때 기본 설정 값은 동적 프로토타입(Dynamic Prototypes)이며, 정적 셀(static cells)도 사용 가능합니다.
  * 셀 하나를 디자인해 이를 다른 셀의 템플릿으로 사용하는 방식
  * 같은 레이아웃의 셀을 여러 개 이용해 정보를 표시할 경우
  * 데이터 소스(UITableViewDataSource) 인스턴스에 의해 콘텐츠를 관리하며, 셀의 개수가 상황에 따라 변하는 경우에 사용
* 구성 요소 : `cell`, `delegate`, `data sourse`  

* [x] **2) 테이블뷰 셀이란?**
* 테이블뷰 셀
  : 테이블뷰를 이루는 개별적인 행(row)
* 테이블뷰 셀의 구조
  * 콘텐츠 영역 
  * 액세서리뷰 영역 : 상세보기, 재정렬, 스위치 등과 같은 컨트롤 객체 위치
  * 편집 모드(editing Mode)로 전환하면 다음과 같이 세 영역으로 나뉩니다.
    * 편집 컨트롤
    * 셀 콘텐츠
    * 재정렬 컨트롤


* [x] **3) DataSource와 Delegate?**
* **MVC에 따르면** 데이터 소스는 M, 데이블뷰는 V, 델리게이트는 C와 가깝습니다. 
* 데이터 소스 (`UITableViewDataSource` 프로토콜)
  *  테이블 뷰를 생성하고 수정하는데 필요한 정보를 테이블뷰 객체에 제공합니다.
  * 데이터 모델의 델리게이트로, 테이블뷰의 시각적 모양에 대한 최소한의 정보를 제공합니다.
  * UITableView 객체에 섹션의 수와 행의 수를 알려주며, 행의 삽입, 삭제 및 재정렬하는 기능을 선택적으로 구현할 수 있습니다.
```swift
 @required 
 // 특정 위치에 표시할 셀을 요청하는 메서드
 func tableView(UITableView, cellForRowAt: IndexPath) 
 // 각 섹션에 표시할 행의 개수를 묻는 메서드
 func tableView(UITableView, numberOfRowsInSection: Int)
```
* 델리게이트(`UITableViewDelegate` 프로토콜)
  * 테이블뷰의 시각적인 부분 수정, 행의 선택 관리, 액세서리뷰 지원 그리고 테이블뷰의 개별 행 편집을 도와줍니다. 

* [x] **4) 간단한 테이블뷰 만들기**

* [x] **5) 테이블뷰에 동적으로 데이터 추가하기** 

* [x] **6) 셀 커스터마이징**

######2. 뷰의 재사용
* [x] **1) 뷰의 재사용이란?**
* 뷰의 재사용
  뷰를 재사용함으로써 메모리를 절약하고 성능 또한 향상할 수 있습니다.
  ex) `UITableViewCell`, `UICollectionViewCell`
* 재사용 원리
  1. 데이터 소스에 뷰(셀) 인스턴스를 요청합니다.
  2. `재사용 큐 (Reuse Queue)`에 재사용을 위해 대기하고있는 셀이 있는지 확인 후 있으면 그 셀에 새로운 데이터를 설정하고, 없으면 새로운 셀을 생성합니다.
  3. 데이터 소스가 셀을 반환하면 화면에 표시합니다.
  4. 스크롤을 하게 되면 일부 셀들이 화면 밖으로 사라지면서 다시 재사용 큐에 들어갑니다.
  -> 위 과정이 계속 반복됩니다 !

* [x] **2) 셀이 재사용되고 있어요**

######3. 스토리보드 세그
* [x] **1) 세그(Segue)란?**
* 세그란? 스토리보드에서 뷰 컨트롤러 사이의 화면전환을 위해 사용하는 객체입니다. 
* UIStoryboardSegue 클래스
  * UIKit에서 사용할 수 있는 표준 화면전환을 위한 프로퍼티와 메서드를 포함하고 있습니다. 
  * 커스텀 전환을 정의하기 위해 서브클래스를 구현해서 사용할 수도 있습니다. 
```swift
//주요 프로퍼티
//세그에 전환을 요청하는 뷰 컨트롤러입니다.
var source: UIViewController
//전환될 뷰 컨트롤러입니다.
var destination: UIViewController
//세그 객체의 식별자입니다.
var identifier: String?
//주요 메서드
//뷰 컨트롤러의 전환을 수행합니다.
func perform()
```

* [x] **2) 다음 화면으로 데이터 전달하기**


######4. JSON 다루기
* [x] **1) Codable**
* 인코딩(Encoding) : 정보의 형태나 형식을 표준화, 보안, 처리 속도 향상, 저장 공간 절약 등을 위해서 다른 형태나 형식으로 변환하는 처리 혹은 그 처리 방식 (부호화)
* 디코딩(Decoding) : 인코딩의 반대 작업을 수행하는 것
* Codable
```swift 
typealias Codable = Decodable & Encodable
```
JSON 형식으로 서버와 애플리케이션이 통신한다면 Codable 프로토콜을 이용해 편리하게 인코딩 및 디코딩할 수 있습니다.
* Codable
  * 다른 데이터 형식으로 변환하고 싶은 경우에 Codable 프로토콜을 준수하도록 하면 됩니다. 
```swift
struct 구조체이름: Codable {
    ...
}
```
* CodingKey
  * JSON 형태의 데이터로 상호 변환하고자 할 때는 기본적으로 인코딩/디코딩할 JSON 타입의 키와 애플리케이션의 사용자정의 프로퍼티가 일치해야 합니다.
  * 만약 JSON의 키 이름을 구조체 프로퍼티의 이름과 다르게 표현하려면 타입 내부에 String 타입의 원시값을 갖는 CodingKeys라는 이름의 열거형을 선언하고 CodingKey 프로토콜을 준수하도록 하면 됩니다. 
  * CodingKeys 열거형 케이스의 이름은 해당 프로퍼티의 이름과 일치해야 합니다. 
  * 프로퍼티의 열거형 케이스의 값으로 매칭할 JSON 타입의 키를 할당하면 됩니다. 이름이 일치한다면 값을 할당하지 않아도 무방합니다.
```swift
struct Landmark: Codable {
    var name: String
    var foundingYear: Int
    var location: Coordinate
    var vantagePoints: [Coordinate]
    
    enum CodingKeys: String, CodingKey {
        case name = "title"
        case foundingYear = "founding_date"
        
        case location
        case vantagePoints
    }
}
```

* [x] **2) JSONEncoder / JSONDecoder**
* 스위프트 4 버전부터 ` JSONEncoder` / `JSONDecoder`가 `Codable` 프로토콜을 지원합니다. (스위프트 4 버전 이전에는 JSONSerialization을 사용해 JSON 타입의 데이터를 생성했습니다. )
* JSONEncoder, JSONDecoder
```swift
struct GroceryProduct: Codable {
    var name: String
    var points: Int
    var description: String?
}

let pear = GroceryProduct(name: "Pear", points: 250, description: "A ripe pear.")

let encoder = JSONEncoder()
// Tip : encoder.outputFormatting = .prettyPrinted 설정하면 들여쓰기를 통해 가독성이 좋게 출력해줍니다.
encoder.outputFormatting = .prettyPrinted

do {
	let data = try encoder.encode(pear)
	print(String(data: data, encoding: .utf8)!)
} catch {
	print(error)
}

// ----- 출력
 {
   "name" : "Pear",
   "points" : 250,
   "description" : "A ripe pear."
 }

/// 스위프트 4 버전부터 """를 통해 여러 줄 문자열을 사용할 수 있습니다.
let json = """
{
    "name": "Durian",
    "points": 600,
    "description": "A fruit with a distinctive scent."
}
""".data(using: .utf8)!

let decoder = JSONDecoder()

do {
	let product = try decoder.decode(GroceryProduct.self, from: json)
	print(product.name)
} catch {
	print(error)
}
// ----- 출력 
"Durian"
```

* [x] **3) JSON 다루기**

######5. Summary
* [x] **1) 돌아보기**











