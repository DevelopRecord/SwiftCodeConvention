# SwiftCodeConvention
나를(내가 보기) 위해 Swift 코드를 명확하고 이해하기 쉽게 일관성 있게 작성하는 방법을 기초적인 내용부터 가볍게 넘어갈 수 있는 부분까지 세세하게 다룹니다.

## 목차

[1. 네이밍](#네이밍)   
[2. 델리게이트](#Delegate)   
[3. 클로저](#클로저)   
[4. 주석](#주석)   
[5. 임포트](#import)   
[6. 줄바꿈](#줄바꿈)   
[7. 기타 사항](#기타-사항)   

#### 네이밍   

* UpperCamelCase
  * 단어의 첫 글자를 모두 대문자로 정의하는 방법
  * Class(객체), Structure(구조체), 열거형(Enumeration), 익스텐션(Extension), 프로토콜(Protocol) 등의 이름을 정의할 때 사용
  * ex) MainController, User, AccountType, UserIndex 등

* lowerCamelCase
  * 단어의 첫 글자를 제외한 단어의 첫 글자는 모두 CamelCase와 동일하게 대문자로 정의하는 방법
  * 변수(Variable), 상수(Constant), 함수(Function), 프로퍼티(Property), 파라미터(Parameter) 등의 이름을 정의할 때 사용
  * ex) user, userIndex, accountType, searchResults 등

* 약어
  * 단어가 약어로 시작하는 경우 소문자로 표기하고 그 외에는 모두 대문자로 표기합니다.

#### 올바른 예   
<pre><code>
let valueID: Int?
let html: String?
let weatherURL: URL?
let urlString: String?
</code></pre>

#### 부적절한 예   
<pre><code>
let valueId: Int?
let HTML: String?
let weatherUrl: URL?
let URLString: String?
</code></pre>

#### Delegate
  * 델리게이트는 프로토콜 명으로 네임스페이스를 구분합니다.
  * 네임스페이스란 소스 코드에 불필요한 명칭 규칙을 사용하지 않아도 이름 충돌이 발생하지 않고 쉽게 설명할 수 있도록 제정된 개념이고 쉽게 설명해서 관련있는 기능들끼리 모아놓은 공간이라는 개념입니다.

#### 올바른 예   
<pre><code>
protocol AuthentificationDelegate {
  func authentificationView()
  func authentificationComplete()
}
</code></pre>

#### 부적절한 예   
<pre><code>
protocol AuthentificationDelegate {
  func setUserName()
  func setUserProfile()
  
  func AuthentificationView() // AuthentificationView라는 뷰가 존재할 경우에는 에러가 발생합니다.
}
</code></pre>

#### 클로저   
- 리턴타입이 없는 클로저를 정의할 때는 <pre><code>(() -> Void)</code></pre> 방식으로 사용합니다.

#### 올바른 예   
<pre><code>
func doSomething(completion: () -> Void) {
  // do something
}
</code></pre>

#### 부적절한 예   
<pre><code>
func doSomething(completion: ()->Void) {
  // do something
}
</code></pre>

#### 주석   
- <pre><code>//</code></pre>를 사용해서 한줄 문서화 주석을 남깁니다.
<pre><code>
// 이름을 가져올 함수
func getName(name: String) {
  // 이름을 보여줄 라벨
  let nameLabel = UILabel()
}
</code></pre>

- <pre><code>///</code></pre>를 사용해서 한줄 문서화 주석을 남깁니다.
<pre><code>
/// 이름을 가져올 함수
func getName(name: String) {
  /// 이름을 보여줄 라벨
  let nameLabel = UILabel()
}
</code></pre>

- <pre><code>// MARK: - </code></pre>를 사용해서 연관되는 코드들을 묶고 구분짓습니다.
<pre><code>
// MARK: - Properties

private let label = UILabel()
private let confirmButton = UIButton()

// MARK: - Lifecycle

override func viewDidLoad() {
    super.viewDidLoad()
    configureUI()
}
</code></pre>

#### import   
- 모듈 임포트는 최상단에 작성하며 알파벳을 기준으로 나열합니다.
- 내장 라이브러리를 먼저 임포트하고 서드파티 라이브러리들을 임포트합니다.
- UIKit을 임포트 해야한다면 Foundation은 지워주도록 합니다.
<pre><code>
import UIKit
import SnapKit
import SwiftyBeaver
import Then
</code></pre>

#### 줄바꿈   
- 코드 안에서는 불필요한 줄바꿈은 하지 않습니다.
- 코드가 없는 빈 줄은 아무것도 없는 공백 상태를 유지합니다.(필수인지는 잘 모르겠음)
- 코드가 끝나는 모든 파일의 마지막 줄은 항상 공백 상태를 유지합니다.
- <pre><code>// MARK: - </code></pre>에는 위, 아래로 공백 상태를 유지합니다.
- 함수 내부 코드는 들여쓰기를 합니다.
<pre><code>
func doSomething(completion: () -> Void) {
  // do something
}
</code></pre>

#### 기타 사항   
- 저는 미처 보지 못한 줄바꿈이나 들여쓰기는 Swimat이라는 프로그램을 사용합니다.
- 클래스에 프로토콜을 적용할 때는 extension을 활용하여 따로 작성합니다.
- 저는 위의 MARK 주석 뿐만 아니라 Helpers, Selectors UITableViewDelegate, UITableViewDataSource 등 기능별로 나눈 주석 예약어를 사용합니다.
- 레이아웃이나 클로저를 통한 인스턴스 생성 시 SnapKit이나 Then을 주로 사용하여 코드의 가독성을 높입니다.
- 중복되는 코드는 리팩토링하여 여러곳에서 사용할 수 있도록 합니다.
<pre><code>
private let previousButton: UIButton = {
  let button = UIButton(type: .system)
  button.tintColor = .systemBlue
  button.titleLabel?.font = UIFont.boldSystemFont(ofSize: 16)
  button.layer.borderWidth = 2
  button.layer.borderColor = UIColor.black.cgColor
  button.layer.cornerRadius = 25
  return button
}()
</code></pre>   
이러한 버튼이 여러개가 있을 때 아래 방식으로 커스텀 버튼을 만들어 여러 곳에서 재사용 가능하게 리팩토링합니다.   
타이틀이나 이미지를 기본값을 설정하여 선택적으로 사용 가능합니다.   
<pre><code>
class ActionButton: UIButton {

  init(title: String? = nil, image: UIImage? = nil) {
      super.init(frame: .zero)

      setTitle(title, for: .normal)
      setImage(image, for: .normal)
      setTitleColor(.white, for: .normal)
      titleLabel?.font = UIFont.boldSystemFont(ofSize: 16)
      layer.borderWidth = 2
      layer.borderColor = UIColor.white.cgColor
      layer.cornerRadius = 25
  }

  required init?(coder: NSCoder) {
      fatalError("init(coder:) has not been implemented")
  }
}
</code></pre>
이후 아래 방식으로 재사용 가능합니다.   

<code><pre>
private let previousButton = ActionButton(title: "이전")
private let nextButton = ActionButton(title: "다음")
</code></pre>
