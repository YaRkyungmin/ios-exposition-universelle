# 🏛️만국박람회
## 🍀 소개 
`yyss99` `kyungmin`이 만든 만국박람회 앱입니다.
`JSON`데이터를 `Decode`해서 `TableView` 와 `ScrollView`를 이용해 박람회에 대한 정보를 보여주는 앱입니다.

## 📖 목차
1. [팀원](#-팀원)
2. [그라운드룰](#-그라운드룰)
3. [일일 스크럼](#-일일-스크럼)
4. [타임라인](#-타임라인)
5. [실행 화면](#-실행-화면)
6. [시각화된 프로젝트 구조](#-시각화된-프로젝트-구조)
7. [트러블 슈팅](#-트러블-슈팅)
8. [프로젝트 회고](#-프로젝트-회고)
9. [참고 링크](#-참고-링크)

<br>

## 👨‍💻 팀원
| yyss99(와이) | kyungmin(경민) |
| :------: | :------: |
|<Img src= "https://hackmd.io/_uploads/Byuz8kh_3.png" width="200"> |<Img src="https://cdn.discordapp.com/attachments/1100965172086046891/1108927085713563708/admin.jpeg" width="200"> |
|[Github Profile](https://github.com/yy-ss99) |[Github Profile](https://github.com/YaRkyungmin)|

<br>
    
## 📝 그라운드룰
- [그라운드룰](https://github.com/yy-ss99/ios-exposition-universelle/wiki/🤙Ground-Rules)
## 🌻 일일 스크럼
- [일일 스크럼](https://github.com/yy-ss99/ios-exposition-universelle/wiki/🌻일일-스크럼)

## ⏰ 타임라인
|날짜|내용|
|:--:|--|
|2023.06.27.(화)| - MVC 단위로 그룹화 <br> - ExpoInformation 타입 생성 및 구현 <br> - DataTransferObject 그룹 생성 <br> - ExpoEntry 타입 구현|
|2023.07.02.(일)| - expo_assets 추가 <br> - ExpoViewController 추가 및 기능 구현 <br> - EntryViewController 추가 및 기능 구현 <br> - Entry TableCell 기능 구현 <br> - EntryDetailViewController 파일 추가|
|2023.07.03.(월)| - 스토리보드 autolayout 제약 수정<br> - EntryDetailViewController entry 사진 및 설명 추가 <br> - ExpoViewController 네비게이션 바 숨기기 기능 추가 <br> - DecodeError 구현 <br> - 프로퍼티 접근제한 및 리팩토링 <br> - NumberFormatter 기능 구현 <br> - 네임스페이스 추가 및 분리
|2023.07.05(화)| - CommaFormatter 수정 및 추가 <br> - EntryTableViewCell에 super.prepareForReuse()추가 <br> - decode 오류 Alert 구현 <br> -EntryDetailViewController 의존성 주입 <br> - ViewController 로직 분리 및 String, Int 확장 |
|2023.07.06(화)| - 스크롤 뷰 제약 수정 <br> - ContainerViewController 화면 고정 기능 추가|


## 📱 실행 화면
|첫 화면|테이블 뷰 화면 |
|:--:|:--:|
|<Img src = "https://hackmd.io/_uploads/HyEa0mHYn.gif" width="400"/>|<Img src = "https://hackmd.io/_uploads/HkqEyVBKh.gif" width="400"/>|
|상세 화면|다이나믹 타입 적용 ||:--:|:--:|
|<Img src = "https://hackmd.io/_uploads/By251NHF3.gif" width="400"/>|<Img src = "https://hackmd.io/_uploads/SyOelNrt3.gif" width="400"/>|
|SE 화면으로 실행| SE 화면 다이나믹 타입 적용||:--:|:--:|
|<Img src = "https://hackmd.io/_uploads/BkrOx4St3.gif" width="400"/>|<Img src = "https://hackmd.io/_uploads/S1MqlNBt3.gif" width="400"/>|

## 👀 시각화된 프로젝트 구조

### 🌟 Class Diagram
![reference link](https://hackmd.io/_uploads/B1R5rEBtn.png)

### 🗂 폴더 구조
> Model : 앱 구동 로직에 필요한 모델
> View : 화면을 구성하는 뷰
> Controller : 화면의 이벤트와 전환을 컨트롤하는 컨트롤러
> App : AppDelegate, SceneDelegate
```
Expo1900 project
└── Expo1900
   ├── App
   │   ├── AppDelegate
   │   └── SceneDelegate
   ├── Model
   │   ├── DataTransferObject
   │   │   │── ExpoInformation
   │   │   └── ExpoEntry
   │   ├── NameSpace
   │   │   │── StoryBoardNameSpace
   │   │   │── AssetsNameSpace
   │   │   └── ExpoInformationNameSpace
   │   ├── AlertController
   │   ├── CommaFormatter
   │   ├── DecodeError
   │   ├── Decoder
   │   └── ExpoInformationSetter
   │── Controller ContainerViewController
   │   ├── EntryTableViewCell
   │   ├── ExpoViewController
   │   ├── EntryViewController
   │   ├── EntryDetailViewController
   │   └── ContainerViewController
   ├── View
   │   ├── Main
   │   └── LaunchScreen
   └── Resource
       ├── Assets
       └── Info
```
## 🧨 트러블 슈팅

### 1️⃣ Data의 상수명 바꾸기
`short_desc`나 `image_name` 같은 스위프트 네이밍과 다른 상수명을 바꾸기 위해서 `CodingKey`를 사용하였습니다.


``` swift
struct ExpoEntry: Decodable {
    let name: String
    let imageName: String
    let shortDescription: String
    let description: String
    
    private enum CodingKeys: String, CodingKey {
        case name
        case imageName = "image_name"
        case shortDescription = "short_desc"
        case description = "desc"
    }
}
```

### 2️⃣ Codable 과 Decodable 어떤 것을 채택 할 것인가

`Codable`은 `Decodable`과 `Encodable`프로토콜을 둘 다 가지고 있어서 데이터를 인코딩하고 디코딩하는데에 사용됩니다. 반면에 `Decodable`프로토콜은 데이터를 디코딩하는데만 사용됩니다. 이번 프로젝트에서는 `JSON`데이터를 디코딩 하는 것만 필요할 것이라고 생각해서 `Decodable`을 채택했습니다.

### 3️⃣ 특정 화면만 세로 화면 고정하기

첫 화면만 세로로 고정하기 위해서 `UIViewController`에 있는 `supportedInterfaceOrientations`라는 `property`를 사용하기로 했습니다.

`supportedInterfaceOrientations`는 기기방향이 변경되면 루트 뷰 컨트롤러 또는 창을 채우는 최상위 모달 뷰 컨트롤러에서 이 메서드를 호출한다고 공식문서에 나와 있었습니다. `view controller`에 상위 `view controller`가 있다면 그 상위 `view controller`의 `porperty`를 따른다고 이해했습니다. `UINavigationController`가 `all`이라면 그 안에 있는 `viewController`들은 `UINavigationController`를 따라 `all`이 됩니다.

    
``` swift
final class ContainerViewController: UINavigationController {
    override var supportedInterfaceOrientations: UIInterfaceOrientationMask {
        guard let supportedInterfaceOrientations = self.topViewController?.supportedInterfaceOrientations else {
            return self.supportedInterfaceOrientations
        }
        
        return supportedInterfaceOrientations
    }
}
```


화면마다 바꾸어주기 위해서 `UINavigationController` 상속받는 `class`를 만들었습니다. 그런 뒤에 가장 최상위 `viewController`의 `supportedInterfaceOrientations` 속성을 `return`하도록 했습니다.

    
``` swift
//  새로로 고정 할 첫 화면
override var supportedInterfaceOrientations: UIInterfaceOrientationMask {
        return .portrait
}

// 회전이 가능하게 할 그 다음 화면
override var supportedInterfaceOrientations: UIInterfaceOrientationMask {
        return .all
}
```


### 4️⃣ 네비게이션 바 색상 변경

스크롤을 내리지 않아도 `Navigation Bar`의 색상이 `default`색으로 보이게하는 방법에 대해 고민했습니다.

스토리보드 상 `inspector`에 있는 `Navigation Bar Appearances`속성에는 다음과 같이 네가지가 있었습니다.

- `Standard`: 일반적인 상태의 `Navigation Bar`를 나타내고 `Navigation Bar`의 높이가 일반적인 크기로 표시되며, 네비게이션 아이템과 타이틀을 포함합니다.
- `Compact`: 네비게이션 바의 크기를 축소하여 표시합니다. `Navigation Bar`의 높이가 줄어들고, 아이템과 타이틀이 더 작은 공간에 표시됩니다.
- `Scroll Edge`: 네비게이션 바가 스크롤 가장자리에 붙도록 지정합니다. 스크롤할 때 `Navigation Bar`가 화면 위쪽으로 이동하여 사라지지 않고 고정됩니다.
- `Compact Scroll Edge`: `Compact`모드에서 `Scroll Edge`모드로 변경될 때 적용되는 속성입니다. `Compact`모드에서 `Navigation Bar`가 축소된 크기로 표시되다가 스크롤시 `Scroll Edge`모드로 전환되면서 `Navigation Bar`의 크기와 레이아웃이 변경됩니다.

이 속성들 중 목적에 맞게 `Scroll Edge`에 대한 속성만 적용하여서 네비게이션 바의 색상이 고정시켰습니다.

### 5️⃣ ScrollView의 autoLayout 설정
처음 `ScrollView`에 대한 제약을 설정해줄 때는 `VerticalStackView`를 바로 `ScrollView`에 담아줬습니다. autoLayout은 잡혔지만 기기를 변경해서 테스트해줄때 가로방향으로도 스크롤이 되는 문제가 생겼습니다. 

`WorkingwithScrollViews`에서 `Add a view to the scroll view. Set the view’s Xcode specific label to Content View.`라는 문장을 보고나서 `ScrollView`에 컨텐츠들을 담기전에 `ContentView`를 먼저 담은 뒤에 그 `ContentView`에 컨텐츠들을 넣어줘야 되는것을 알게 됐습니다. 

가로방향으로만 스크롤이 되게 할 때는 `ConteneView`의 `height`를 `ScrollView`의 `FrameLaout height`와 같게 해주면 됐고, 세로방향으로만 스크롤이 되게 할때는 `ConteneView`의 `width`를 `ScrollView`의 `FrameLaout width`와 같게 해주면 된다는 것도 알게 되었습니다.

### 6️⃣ Decoder 파일의 위치 

`JSON`파일명을 입력받아 디코딩해주는 `Decoder`객체의 파일의 위치는 `Model`에 있어야 한다고 생각했습니다. 하지만 `NSDataAsset` 클래스를 사용하기 위해 `UIKit`모듈을 `import` 해줘야 해서 Model안의 파일이 `UIKit`을 `import`해줘도 되는지 의문점이 들었습니다. 여러 문서를 찾아보고 `Model`은 `View`를 몰라야 한다는 것을 깨달았습니다. 그런데 이건 어디까지를 `View`로 볼것이냐부터 정해야 한다는 기준에 의해서 정하는 것 같습니다. `MVC`를 나눌때의 나름의 기준을 세우는 것이 맞다고 판단했습니다.

### 7️⃣ 화면 간 값 전달 시 의존성 주입 

```swift
//EntryDetailViewController
final class EntryDetailViewController: UIViewController {
    @IBOutlet private weak var entryImageView: UIImageView!
    @IBOutlet private weak var entryDescription: UILabel!

    var expoEntry: ExpoEntry?
		...
}

//EntryViewController
final class EntryViewController: UIViewController {
    ....
}

extension EntryViewController: UITableViewDataSource, UITableViewDelegate {
		func tableView(_ tableView: UITableView, didSelectRowAt indexPath: IndexPath) {
        let expoEntry = self.expoEntries[indexPath.row]
        guard let entryDetailViewController = storyboard?.instantiateViewController(withIdentifier: StoryBoardNameSpace.entryDetailViewController) as? EntryDetailViewController else { return }
        entryDetailViewController.expoEntry = expoEntry
        navigationController?.pushViewController(entryDetailViewController, animated: true)
    }
}
```

해당코드에서 `expoEntry`는생성자를 통해 주입해주면 외부에서 몰라도 되는 정보라고 판단했습니다. 또한 옵셔널이 아니어도 될 것 같아 `instantiateViewController(identifier:creator:)`를 활용해 봤습니다.

```swift
//EntryDetailViewController
final class EntryDetailViewController: UIViewController {
    private var expoEntry: ExpoEntry
    
    @IBOutlet private weak var entryImageView: UIImageView!
    @IBOutlet private weak var entryDescription: UILabel!
    
    override var supportedInterfaceOrientations: UIInterfaceOrientationMask {
        return .all
    }
    
    init?(expoEntry: ExpoEntry, coder: NSCoder) {
        self.expoEntry = expoEntry
        super.init(coder: coder)
    }
    
    required init?(coder: NSCoder) {
        fatalError("init(coder:) has not been implemented")
    }
		....
}

//EntryViewController
final class EntryViewController: UIViewController {
    ....
}

extension EntryViewController: UITableViewDataSource, UITableViewDelegate {
			...    
    func tableView(_ tableView: UITableView, didSelectRowAt indexPath: IndexPath) {
        let expoEntry = self.expoEntries[indexPath.row]

        guard let entryDetailViewController = storyboard?.instantiateViewController(identifier: StoryBoardNameSpace.entryDetailViewController, creator: {
            coder in EntryDetailViewController(expoEntry: expoEntry, coder: coder)}) else { return }
        
        navigationController?.pushViewController(entryDetailViewController, animated: true)
    }
}
```

## 👥 프로젝트 회고
### 잘한 부분 👍🏻
- 그라운드 룰을 잘 지켰습니다.
- 서로에 대한 배려와 존중을 지켜주었습니다.
- 주장과 논리에 확실한 근거가 있으면 서로의 의견을 통합하고 더 좋은 방향으로 이끌어 나갔습니다.
- 이해가 가지 않는 부분은 서로가 서로에게 질문하고 답하기를 반복하며 공부했습니다.
- 기억보단 기록에 포커스를 두어서 최대한 기록하려 노력했습니다.
- 도큐먼트의 내용을 이해하고 적용하도록 노력했습니다.

### 부족한 부분 🫣
- 오토레이아웃에 대한 개념이 확실하게 잡혀있지 않은 상태로 프로젝트에 도입하려 했지만, 후에 다시 제대로 공부하고 도큐먼트 가이드라인에 따라 오토레이아웃을 적용하려고 노력했습니다.

## 📚 참고 링크
[🍎Apple Docs: JSONDecoder](https://developer.apple.com/documentation/foundation/jsondecoder)
[🍎Apple Docs: Using JSON with Custom Types](https://developer.apple.com/documentation/foundation/archives_and_serialization/using_json_with_custom_types)
[🍎Apple Docs: Encoding and Decoding Custom Types](https://developer.apple.com/documentation/foundation/archives_and_serialization/encoding_and_decoding_custom_types)
[🍎Apple Docs: UINavigationController](https://developer.apple.com/documentation/foundation/archives_and_serialization/encoding_and_decoding_custom_types)
[🍎Apple Docs: UITableViewDelegate](https://developer.apple.com/documentation/uikit/uitableviewdelegate)
[🍎Apple Docs: UITableViewDataSource](https://developer.apple.com/documentation/uikit/uitableviewdatasource)
[🍎Apple Docs: supportedInterfaceOrientations](https://developer.apple.com/documentation/uikit/uiviewcontroller/1621435-supportedinterfaceorientations)
[🍎Apple Docs: UIInterfaceOrientationMask](https://developer.apple.com/documentation/uikit/uiinterfaceorientationmask)
[🍎Apple Docs: WorkingwithScrollViews](https://developer.apple.com/library/archive/documentation/UserExperience/Conceptual/AutolayoutPG/WorkingwithScrollViews.html)
[🍎Apple Docs: Customize the Navigation Bar Appearance](https://developer.apple.com/documentation/uikit/uinavigationcontroller/customizing_your_app_s_navigation_bar#3950605)
