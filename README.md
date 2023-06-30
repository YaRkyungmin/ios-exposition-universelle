# 🏛️만국박람회
## 🍀 소개 
`yyss99` `kyungmin`이 만든 만국박람회 앱입니다.
`JSON`데이터를 `Decode`해서 `TableView` 와 `ScrollView`에 뿌려주는 앱입니다.

## 📖 목차
1. [팀원](#-팀원)
2. [그라운드룰](#-그라운드룰)
3. [일일 스크럼](#-일일-스크럼)
4. [타임라인](#-타임라인)
5. [트러블 슈팅](#-트러블-슈팅)
6. [참고 링크](#-참고-링크)

<br>

## 👨‍💻 팀원
| yyss99(와이) | kyungmin |
| :------: | :------: |
|<Img src= "https://hackmd.io/_uploads/Byuz8kh_3.png" width="200"> |<Img src="https://cdn.discordapp.com/attachments/1100965172086046891/1108927085713563708/admin.jpeg" width="200"> |
|[Github Profile](https://github.com/yy-ss99) |[Github Profile](https://github.com/YaRkyungmin)|

<br>
    
## 📝 그라운드룰
- [그라운드룰](https://github.com/yy-ss99/ios-exposition-universelle/wiki/🤙Ground-Rules)
## 📝 일일 스크럼
- [일일 스크럼](https://github.com/yy-ss99/ios-exposition-universelle/wiki/🌻일일-스크럼)


## ⏰ 타임라인
|날짜|내용|
|:--:|--|
|2023.06.27.(화)| - MVC 단위로 그룹화 <br> - ExpoInformation 타입 생성 및 구현 <br> - DataTransferObject 그룹 생성 <br> - ExpoEntry 타입 구현|


 
## 🧨 트러블 슈팅

### 1️⃣Data의 상수명 바꾸기
`short_desc`나 `image_name` 같은 스위프트 네이밍과 다른 상수명을 바꾸기 위해서 `CodingKey`를 사용하였습니다.

<details> 
<summary>코드</summary>
    
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
</details>

### 2️⃣Codable 과 Decodable 어떤 것을 채택 할 것인가

`Codable`은 `Decodable`과 `Encodable`프로토콜을 둘 다 가지고 있어서 데이터를 인코딩하고 디코딩하는데에 사용됩니다. 반면에 `Decodable`프로토콜은 데이터를 디코딩하는데만 사용됩니다. 이번 프로젝트에서는 `JSON`데이터를 디코딩 하는 것만 필요할 것이라고 생각해서 `Decodable`을 채택했습니다.

## 📚 참고 링크
[🍎Apple Docs: JSONDecoder](https://developer.apple.com/documentation/foundation/jsondecoder)
<br>
[🍎Apple Docs: Using JSON with Custom Types](https://developer.apple.com/documentation/foundation/archives_and_serialization/using_json_with_custom_types)
<br>
[🍎Apple Docs: Encoding and Decoding Custom Types](https://developer.apple.com/documentation/foundation/archives_and_serialization/encoding_and_decoding_custom_types)
