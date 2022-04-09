>프로젝트 기간 2022.02.08 ~ 2022.02.11
>
>팀원 : [Tiana](https://github.com/Kim-TaeHyun-A), [Eddy](https://github.com/kimkyunghun3) / 리뷰어 : [숲재](https://github.com/forestjae)


## 목차

- [프로젝트 소개](#프로젝트-소개)
- [프로젝트 시연](#프로젝트-시연)
- [FlowChart](#Flow-Chart)
- [개발환경 및 라이브러리](#개발환경-및-라이브러리)
- [키워드](#키워드)
- [고민한점](#고민한점)
- [구현사항](#구현사항)
- [배운개념](#배운개념)

## 프로젝트 소개
숫자 야구 게임

## 프로젝트 시연
![](https://i.imgur.com/uaMOjcb.gif)

![](https://i.imgur.com/Cq17izE.gif)

![](https://i.imgur.com/y7tNUcg.gif)

## Flow Chart
![image](https://user-images.githubusercontent.com/52434820/162562757-fb581aa6-7a92-42be-9aac-1c01296fecd8.png)

## 개발환경 및 라이브러리
[![swift](https://img.shields.io/badge/swift-5.6-orange)]()
[![xcode](https://img.shields.io/badge/Xcode-13.3-blue)]()

## 키워드
`git commit` `optional` `collection type` `naming` `고차함수` `메서드 분리`

## 고민한점
* 네이밍
* 옵셔널 처리
* magic number 처리
* 고차함수
* 기능별 method 분리
* Character 사용
* 배열 활용법

자세한 고민 보기

[STEP 1 PR](https://github.com/yagom-academy/ios-number-baseball/pull/80)

[STEP 2 PR](https://github.com/yagom-academy/ios-number-baseball/pull/90)

## 구현사항

Const: 전역으로 사용할 상수들 열거형 

chooseMenu() : 메뉴 선택 함수

checkUserChoice(userInput: String) : 메뉴 선택 확인 함수

startGame() : 프로그램 시작 함수

startUserInput() -> [Int] : 유저가 입력값 넣는 함수

printUserInputGuide() : 유저 입력 값 넣는 가이드 제공 함수

makeThreeRandomNumbers() -> [Int] : 랜덤 값 3개 뽑아내는 함수

convertUserInput() -> [String] : 유저 입력값 형식 변환 함수

checkUserNumberFormat(userInput: [String]) -> [Int] : 유저 입력값 유효성 검사 함수

isStringFormat(userInput: [String]) -> Bool : String 형식 확인 함수

isThreeDigits(userInput: [String]) -> Bool : 3개 숫자 확인 함수

isSameCharacter(userInput: [String]) -> Bool : 동일한 Char인지 확인 함수

convertType(of userInput: [String]) -> [Int] : Int 배열 만드는 함수

checkStrike(userStrikeCount: Int, userNumbers: [Int]) -> ([Int], Int) : Strike 확인하는 함수

countStrike(userNumber: Int, userIndex: Int, userStrikeCount: Int) -> (Int?, Int)? : Strike count 함수

checkBall(notStrikeNumbers: (numbers: [Int], strikeCount: Int), userBallCount: Int) -> (Int, Int) : 볼 인지 확인하는 함수

countBall(userNumber: Int, userBallCount: Int) -> Int : 볼 count 함수

printResult(userStrikeCount: Int, userBallCount: Int) : 결과 출력 함수

printWinner(userStrikeCount: Int) : 승자 판별해서 출력

## 배운개념
### 네이밍
[영어로 네이밍하는 방법](https://tv.naver.com/v/4980432/list/267189)

리뷰어가 제공해주신 동영상과, API Design Guidelines 를 학습해서 이 기반에 맞게 네이밍을 작성하려고 했다.
먼저 메서드는 동사로 시작하고, 변수나 상수는 명사로 만들도록 했다.
그리고 코드는 하나의 문장처럼 되도록 해야한다. 예를 들어 view.insertSubview(gradientView, at: 2) 이렇게 작성하면 처음부터 주어 - 동사 - 목적어 - 어떻게 순으로 작성되도록 한다.
또한 단수와 복수에 대한 구분도 정확하게 할 필요 있다. album이 한개면 단수, 복수면 albums로 작성해서 혼동을 주지 않는게 좋다.
실제 코드에서도 `makeThreeRandomNumbers`라고 메서드 작성하며 복수형으로 명확하게 표현하려고 한다.
Bool로 반환값을 가지는 메서드는 is~를 사용하도록 한다. 실제 사용하는 메서드를 보면 `isStringFormat` , `isThreeDigits` , `isSameCharacter`  활용해서 Bool 메서드 인것을 보여준다.

### 옵셔널 처리
옵셔널 처리 하는 방법으로는 강제 추출, 옵셔널 바인딩, 닐-병합, 옵셔널 체이닝 등이 있다.
프로젝트 진행 시, 강제 추출은 옳지 않는 방법이라고 생각했고 주로 사용한 것은 옵셔널 바인딩, 닐-병합을 사용하게 되었다.
```swift=
notStrikePossibleBallNumbers.append(notStrikeNumber ?? Const.initCount)
```
와 같은 코드를 적어서 닐-병합을 사용했다.
```swift=
guard let _ = Int(inputWithoutSpace) else {
        return false
    }

if let (notStrikeNumber, strikeCount) = countStrike(userNumber: userNumber, userIndex: userIndex, userStrikeCount: currentStrikeCount) {
    currentStrikeCount = strikeCount
    notStrikePossibleBallNumbers.append(notStrikeNumber ?? Const.initCount)
}
```
옵셔널 바인딩을 위와 같은 방식으로도 사용했다! 그래서 쉽게 옵셔널을 풀 수 있는 것에 대해 배우게 되었다.

### if let vs guard let
if는 지역 변수고 guard는 전역 변수로 사용될 수 있다.
guard는 eraly exit을 위해 사용되기에 메서드 앞쪽에 위치하는 것이 좋다.

### Character 활용
[Character.init](https://developer.apple.com/documentation/swift/character)

Character는 String을 사용해서만 인스턴스를 생성할 수 있다.
```swift=
inputWithoutSpace.contains(Character(String(Const.initCount)))
```
위 코드에서 `Const.initCount` 는 Int이다.

### 전역 변수 제거
전역 변수를 사용하지 않기 위해 매개변수를 통해 값을 받도록 했다.
전역 변수롤 사용됐던 값을 수정해야 해서 리턴에 튜플을 사용해서 처리했다.

### magic number 처리
Enum namespace를 활용해서 재사용성 가능한 상수들을 처리할 수 있다. 이를 통해 magic number를 없애고 어떤 상수인지 다른 사람이 보았을 때 가독성이 더 높아진 것 같았다.

### method 책임 분리
기능별로 method를 분리해서 각 메서드마다 책임을 부여했다. 이로 인해 각 메서드간의 자율성이 높아지고 책임을 분산시킬 수 있었다.
하지만 초반 설계의 문제점으로 인해 하나의 기능만 수행하지 않는 메서드가 생겨서 이를 사용하는 것과 네이밍을 짓는데 어려움을 겪었다.


### 고차함수
compactMap 을 사용해서 특정 조건을 만족하는 element만 뽑아낼 수 있다.
```swift=
let result: [Int] = userInput.compactMap {
        Int(String($0))
}
```

map 을 사용해서 반복해서 element에 접근해서 배열을 뽑아냈다.
```swift=
let userThreeNumbers = userInput.map { String($0) }
```

### enumerated()
배열을 반복문으로 접근할 때 인덱스와 값을 튜플로 얻을 수 있다.
```swift=
for (userIndex, userNumber) in userNumbers.enumerated() {
    ...
}
```
