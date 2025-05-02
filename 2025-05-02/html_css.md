# HTML + CSS

## Before After 가상 클래스

### 배경 이미지에 div 오버레이 사용하기

!! border 그려서 확인해보는 습관 필요

```css
/* HTML
<div class="image-frame">
  <h1>Budapest in Hungary</h1>
</div>
*/

.image-frame {
  width: 800px;
  height: 500px;
  background: url(images/budapest.jpg) no-repeat center center;
  background-size: cover;
  position: relative;
}
/* after로 했을 경우 h1이 뒤로 가려질 수 있음. 그럴 경우 z-index 추가도 고려 */
.image-frame::before {
  content: "";
  position: absolute;
  width: 100%;
  height: 100%;
  background: linear-gradient(to right bottom, crimson, transparent);
}
.image-frame h1 {
  font-size: 3.5em;
  color: #fff;
  position: relative;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  text-align: center;
}
```

### :before :after 속성을 선택하는 content 함수(attr)

```css
선택자:before {
	/*content: attr(속성이름);*/
	content: attr(data-text);
}

/* 사용자 정의 속성 */
<a href="#none" data-text="test">...</a>
```

```css
/* HTML
<div class="notice" data-count="12">
  <i class="fa fa-bell-o"></i>
</div>
*/    

/* icon은 :before, :after를 가질 수 없기 때문에 div로 감싸줌 */
.notice {
  display: inline-block;
  position: relative;
}
.notice:before {
  content: attr(data-count);
  position: absolute;
  background-color: red;
  color: #fff;
  width: 100px;
  height: 100px;
  border-radius: 50%;
  font-size: 50px;
  text-align: center;
  line-height: 100px;
  top: -35px;
  right: -15px;
  border: 5px solid #ddd;
}
.notice .fa {
  font-size: 150px;
}
```

### 사용자 정의 속성과 attr 함수 - Swap Hover Button

```css
/* HTML 
<a href="#" class="cool-btn" data-text="CodingWorks Class"></a>
*/

.cool-btn {
  width: 200px;
  height: 40px;
  line-height: 38px;
  display: block;
  font-size: 15px;
  text-transform: uppercase;
  text-align: center;
  color: #fff;
  text-decoration: none;
  position: relative;
  overflow: hidden;
}
.cool-btn:before,
.cool-btn:after {
  content: attr(data-text);
  width: 100%;
  height: 100%;
  position: absolute;
  transition: 0.35s;
}
.cool-btn:before {
  background-color: crimson;
  top: 0;
  left: 0;
}
.cool-btn:after {
  background-color: royalblue;
  top: 100%;
  left: 0;
}
.cool-btn:hover:before {
  top: -100%;
}
.cool-btn:hover:after {
  top: 0;
}

```

### 자동 Numbering 하는 counter 함수

CSS 카운터 속성 설명

counter-reset : 카운터 이름 시작값; ⇒ 상위 요소에 선언(가급적 부모 요소에 선언)

counter-increment : 카운터이름 증감간격; ⇒  :before 또는 :after에 선언

content : counter(카운터이름);  ⇒ :before 또는 :after에 선언

문자열

content: counter(카운터이름) ‘문자열’;

```css
/* HTML
<!-- ol로는 원하는 디자인의 Bullet을 만들 수 없음 -->
<ul class="items">
  <li>Nitro Cold Brew</li>
  <li>Caffeine Free</li>
  <li>Iced Coffee</li>
  <li>Specialty Coffee</li>
  <li>Brewed Coffee</li>
  <li>Iced Americano</li>
</ul>
*/

/* 부모 요소에 counter-reset */
.items {
  list-style: none;
  /* line-height: 2em; */
  font-size: 18px;
  counter-reset: numbering;
}
.items li:before {
  counter-increment: numbering;
  content: counter(numbering);
  width: 20px;
  height: 20px;
  display: inline-block;
  background-color: crimson;
  color: #fff;
  font-size: 12px;
  text-align: center;
  border-radius: 50%;
  margin-right: 5px;
  transform: translateY(-2px);
}
```

### 리뷰 헤더 UI 디자인(애니메이션 포함)

```css
/* HTML
<h1 class="heading">
  <span>희망을 품게 하는 퍼블리싱 강의</span> 코딩웍스 인프런 수강생
  <em>생생</em> 후기
</h1>
*/

body {
  margin: 0;
  color: #222;
  font-weight: 300;
}

.heading {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  margin: 0;
  text-align: center;
  width: 700px;
  font-size: 38px;
}
.heading:before,
.heading:after {
  position: absolute;
  color: #ddd;
  font-size: 110px;
  top: -40px;
}
.heading:before {
  content: "{";
  left: 0;
}
.heading:after {
  content: "}";
  right: 0;
}
.heading span {
  display: block;
  font-weight: normal;
  font-size: 30px;
  margin-bottom: 10px;
}
.heading span:before {
  content: "\f004";
  font-family: fontawesome;
  margin-right: 5px;
  color: crimson;
  animation: heart 0.7s linear infinite;
  display: inline-block;
}
.heading em {
  font-style: normal;
  color: crimson;
}

@keyframes heart {
  0% {
    transform: scale(0.7);
  }
  50% {
    transform: scale(1.2);
  }
  100% {
    transform: scale(0.7);
  }
}
```

### 폼 요소에 대한 기본적인 이해도

### 필수 폼 가상 클래스, 로그인 폼 CSS 디자인

```css
/* HTML
  <div class="login">
    <div class="field">
      <b>아이디</b>
      <input type="text" placeholder="아이디 입력" />
    </div>
    <div class="field">
      <b>이메일</b>
      <input type="email" placeholder="이메일 입력" />
    </div>
    <div class="field">
      <b>비밀번호</b>
      <input type="password" placeholder="비밀번호 입력" />
    </div>
    <div class="field">
      <b>하고 싶은 말</b>
      <textarea></textarea>
    </div>
    <div class="field user-check">
      <input type="checkbox" checked /> 이벤트 메일 수신에 동의합니다.
    </div>
    <div class="field user-check">
      개인정보 처리방침 약관 동의
      <input type="radio" name="agree" /> 동의함
      <input type="radio" name="agree" />동의 안함
    </div>
    <button>회원가입 하기</button>
  </div>
*/

* {
  box-sizing: border-box;
}

body {
  margin: 50px;
}

.login {
  width: 420px;
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0 0 15px rgba(0, 0, 0, 0.1);
  background-color: #fff;
}
.login b {
  display: block;
  font-weight: 500;
  margin-bottom: 5px;
}
.login .field {
  margin: 10px 0;
}
.login .field.user-check {
  text-align: center;
  font-size: 15px;
}
.login .field input[type="text"],
.login .field input[type="email"],
.login .field input[type="password"],
.login .field textarea {
  width: 100%;
  padding: 8px;
  border: 1px solid #ddd;
  border-radius: 3px;
  outline: none;
}
.login .field textarea {
  height: 100px;
}
.login button {
  width: 100%;
  border: none;
  padding: 7px;
  background-color: limegreen;
  color: white;
  cursor: pointer;
}

```

### 로그인 폼 CSS 디자인 2

```css
/* HTML
<div class="login">
  <div class="field">
    <b>아이디</b>
    <input type="text" placeholder="아이디 입력" />
  </div>
  <div class="field">
    <b>이메일</b>
    <input type="email" placeholder="이메일 입력" />
  </div>
  <div class="field">
    <b>비밀번호</b>
    <input type="password" placeholder="비밀번호 입력" />
  </div>
  <div class="field">
    <select>
      <option value="" selected>회원 가입경로를 선택해주세요.</option>
      <option value="">마케팅</option>
      <option value="">제휴회사</option>
      <option value="">세미나</option>
      <option value="">기타</option>
    </select>
  </div>
  <div class="field">
    <b>하고 싶은 말</b>
    <textarea placeholder="200자 이내로 적어주세요."></textarea>
  </div>
  <div class="field user-check">
    <input type="checkbox" checked /> 이벤트 메일 수신에 동의합니다.
  </div>
  <div class="field user-check">
    개인정보 처리방침 약관 동의
    <input type="radio" name="agree" /> 동의함
    <input type="radio" name="agree" />동의 안함
  </div>
  <button>회원가입 하기</button>
</div>
*/

* {
  box-sizing: border-box;
}
body {
  margin: 50px;
}
.login {
  width: 420px;
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0 0 15px rgba(0, 0, 0, 0.1);
  background-color: #fff;
}
.login b {
  display: block;
  font-weight: 500;
  margin-bottom: 5px;
}
.login .field {
  margin: 10px 0;
}
.login .field.user-check {
  text-align: center;
  font-size: 15px;
}
.login .field input[type="text"],
.login .field input[type="email"],
.login .field input[type="password"],
.login .field select,
.login .field textarea {
  width: 100%;
  padding: 8px;
  border: 1px solid #ddd;
  border-radius: 3px;
  outline: none;
  /* transition: 0.5s; */
}
.login .field textarea {
  height: 100px;
}
.login button {
  width: 100%;
  border: none;
  padding: 7px;
  background-color: limegreen;
  color: white;
  cursor: pointer;
}
/* Form Element Hover Effect*/
/* .login .field input[type="text"]:hover,
.login .field input[type="email"]:hover,
.login .field input[type="password"]:hover {
  border: 1px solid limegreen;
} */
.login .field input[type="text"],
.login .field input[type="email"],
.login .field input[type="password"] {
  padding-left: 35px;
  background-repeat: no-repeat;
  background-position: center left 5px;
}
/* Form Element Icon Image */
.login .field input[type="text"] {
  background-image: url(images/icon-user.png);
  background-size: 22px;
}
.login .field input[type="email"] {
  background-image: url(images/icon-email.png);
  background-size: 20px;
}
.login .field input[type="password"] {
  background-image: url(images/icon-password.png);
  background-size: 20px;
}
/* Form Placeholder CSS */
.login .field input[type="text"]::placeholder,
.login .field input[type="email"]::placeholder,
.login .field input[type="password"]::placeholder,
.login .field select::placeholder {
  color: #bbb;
}
/* 사용자가 클릭했을 때.. Focus CSS*/
.login .field input[type="text"]:focus,
.login .field input[type="email"]:focus,
.login .field input[type="password"]:focus,
.login .field input[type="textarea"]:focus,
.login .field select:focus,
.login .field textarea:focus {
  border: 1px solid limegreen;
}
.login .field input[type="text"]:focus::placeholder,
.login .field input[type="email"]:focus::placeholder,
.login .field input[type="password"]:focus::placeholder,
.login .field textarea:focus::placeholder {
  /* display:none을 제외하고 둘 중 하나를 사용하면 된다. */
  opacity: 0;
  /* visibility: hidden; */
}
```

### 로그인 폼 CSS 디자인 3

checkbox, radio ⇒ label로 묶으면 텍스트를 클릭해도 체크할 수 있다.

or 커스텀하게 만들기

```css
/* HTML
<div class="field user-check">
  <label>
    <input type="checkbox" name="event" checked /><em></em> 이벤트 메일
    수신에 동의합니다.
  </label>
</div>

<div class="field user-check">
  개인정보 처리방침 약관 동의
  <label><input type="radio" name="agree" /><em></em><span>동의함</span></label>
  <label><input type="radio" name="agree" /><em></em><span>동의 안함</span></label>
</div>
*/

/* Custom Checkbox & Radio */
.login .field input[name="event"] {
  display: none;
}
.login .field input[name="event"] + em {
  /* border: 1px solid #000; */
  display: inline-block;
  width: 18px;
  height: 18px;
  margin-right: 5px;
  background: url(images/checkbox-03.png) no-repeat;
  background-position: left;
  transform: translateY(3px);
}

.login .field input[name="event"]:checked + em {
  /* border: 1px solid #000; */
  background-position: right;
}

.login .field input[name="agree"] {
  display: none;
}
.login .field input[name="agree"] + em {
  display: inline-block;
  width: 18px;
  height: 18px;
  margin-right: 5px;
  background: url(images/radio-01.png) no-repeat;
  transform: translateY(3px);
}
.login .field input[name="agree"]:checked + em {
  background-position: right;
}
.login .field input[name="agree"]:checked + em + span {
  color: crimson;
}
```

### input에 폰트 아이콘 사용하기

### 유효성 검사 가상 클래스, 기타 가상 클래스

:valid :invalid - 유효성 체크 가상 클래스

:required - 필수 입력 속성이 지정된 input, select, textarea 선택자로 사용

:enabled :disabled - 활성화 및 비활성화(선택, 클릭, 입력 불가)된 요소를 선택자로 사용

:read-write :read-only - 읽고 쓰기 & 읽기 전용(input, textarea)인 경우에 선택자로 사용

### 특정 선택자 제외하는 not

```css
/* HTML 
<div class="frame1">
  <p>CodingWorks</p>
  <p class="active">HTML+CSS+JS</p>
</div>
*/

.frame1 p:not(.active, .amuguna) {
  font-size: 2em;
  color: red;
}
```

```css
/* HTML
<ul>
  <li>Item 1</li>
  <li>Item 2</li>
  <li>Item 3</li>
</ul>
*/

/* 맨 처음 리스트의 왼쪽만 border-left를 안 주게 하는 방법
   물론 not을 쓰지 않고도 구현은 가능하다
*/
ul {
  display: flex;
  list-style: none;
  padding: 0;
  margin: 0;
}
ul li {
  float: left;
  padding: 0 20px;
}

ul li:not(:first-child) {
  border-left: 1px solid crimson;
}

form input:not(input[type=checkbox], input[type=radio]):focus {
	...
}
```

### 선택자 중복을 줄이는 is

```css
/* HTML 
<header>
  <h1>Headline in header</h1>
</header>
<section>
  <h1>Headline in section</h1>
</section>
<footer>
  <h1>Headline in footer</h1>
</footer>
*/

/* header h1,
section h1,
footer h1 {
  font-size: 2em;
  text-align: center;
  position: relative;
  padding-bottom: 10px;
}
header h1:before,
section h1:before,
footer h1:before {
  content: "";
  position: absolute;
  width: 100px;
  height: 4px;
  background-color: limegreen;
  bottom: 0;
  left: 50%;
  transform: translateX(-50%);
} */

/* 위 선택자들을 is를 통해서 간결하게 작성할 수 있음 */
:is(header, section, footer) h1 {
  font-size: 2em;
  text-align: center;
  position: relative;
  padding-bottom: 10px;
}
:is(header, section, footer) h1:before {
  content: "";
  position: absolute;
  width: 100px;
  height: 4px;
  background-color: limegreen;
  bottom: 0;
  left: 50%;
  transform: translateX(-50%);
}
```