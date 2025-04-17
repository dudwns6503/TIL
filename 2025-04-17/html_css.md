# HTML + CSS

## 태그(HTML Tag) vs 요소(HTML Element)의 차이점?

Tag : h1,h2,h3,h4,h5,h6

Element : 현재 HTML 문서에 사용된 태그

```css
/*
  기본 선택자
*/

h1 {
	color: red;
}

.blue-text {
	color: blue;
}

.ul li {
	color: pink;
}

#green-text {
	color: green;
}
```

```css
/*
  결합 선택자
  스페이스 : 자손 선택자(하위선택자)
  > : 자식 선택자
  , : 연결 선택자(그룹 선택자)
*/

div span {
	color: red;
}

/* 가독성 고려 엔터 */
.start div p,
.end {
	color: red;
}

.end {
	text-transform: uppercase;
}
```

```css
/*
   클래스 중첩해서 사용하기(CSS : Cascading Style Sheet)
*/
/* HTML */
<p class="text-center">Center</p>
<p class="text-center text-large">Center & Large</p>
<p class="text-center text-large text-blue">Center & Large & Blue</p>

/* CSS */
p {
	border: 1px solid #000;
}
.text-center {
	text-align: center;
}
.text-large {
	font-size: 2em;
}
.text-blue {
	color: blue;
}
```

```css
/*
   * : 전체 선택자
*/

/* 
   모든 애들이 가지고 있는 margin이 0이 됨.(좋지 않다!!)
   font-family, box-sizing, outline 만 한다.
*/
* {
  margin: 0;
  padding: 0;
}

======
/*
   body에 font-family를 주면 form 요소는 글꼴이 반영되지 않는다.
   box-sizing을 안 주게 되면 테두리 굵기가 width와 height에 영향을 줌
   outline : 입력 form 같은 것을 눌렀을 때 테두리가 굵어지는 부분들이 있음.(기본으로)
             이를 none으로 지정해서 없애준다.
*/
* {
  font-family: 'Montserrat', 'sans-serif';
  box-sizing: border-box;
  outline: none;
}
```

```css
/*
  태그와 함께 사용하는 선택자(태그.클래스네임)
  좀 더 명확하게 선택할 수 있다.
*/
section.about {
	background-color: blue;
}

```

## 선택자 적용 우선순위

1. !important Style
2. Inline Style
3. ID Selector Style
4. Class Selector Style
5. Tag Selector Style

**중요 : PC 버전의 선택자와 미디어쿼리 구문 내의 선택자 방식을 동일하게 해야 한다.**

```css
h1 {
	color: red !important;
}

section.about {
	background-color: crimson;
	color: #fff;
	padding: 25px;
}

/* HTML에 viewport Meta가 있어야 media query 적용할 수 있다 */
@media (max-width:768px) {
	section.about {
		background-color: yellowgreen;
		color: #000;
	}
}
```

같은 조건일 경우 외부 style.css와 내부 <style> 중에서 내부가 더 우선순위가 높다!

## 인접 형제 선택자

인접 선택자 : + 사용(plus)

형제 선택자 : ~ 사용(tild)

중요 : 인접 형제 선택자를 사용할 경우 형제 요소 기준 아래 요소만 선택 가능(위의 요소 선택 불가)

```css
/* ul을 기준으로 가장 인접한 p 선택*/
ul + p {
	color: red;
}

/* ul을 기준으로 형제 p 모두 선택 */
ul ~ p {
	color: red;
}
```

```css
/*
   :checked 가상 클래스를 통해서 radio, checkbox에 이벤트를 준다
*/

/* HTML
<input type="radio" name="grade"><span>초등학생</span>
<input type="radio" name="grade"><span>중학생</span>
<input type="radio" name="grade"><span>고등학생</span>
<input type="radio" name="grade"><span>대학생</span>
*/

/* ~ span을 사용하면 전체 글씨가 굵게됨*/
input[type=radio]:checked + span {
		font-weight: bold;
}
```

## 속성 선택자(attribute selectors)

### 속성 선택자 기본 형식

속성 : property, attribute

선택자[속성명=”값”]

선택자[속성명=’값’]

선택자[속성명=값]

[속성명=”값”]

속성 선택자 대부분은 form 요소와 관련이 있다.

```css
/* HTML
<div class="login">
	<input type="text" >
	<input type="email" >
	<input type="password" >
	<button>Login</button>
	<label>
	  <input type="checkbox"> <span></span>
	</label>
	<label>
	  <input type="radio"> <span></span>
	</label>
</div>

*/

/* 별도의 클래스를 지정하지 않고도 선택할 수 있음 */
.login input[type=text],
.login input[type=email],
.login input[type=password] {
	width: 100%;
	margin: 5px 0;
	border: 1px solid #ddd;
	padding: 5px;
	border-radius: 5px;
	padding-left: 32px;
	background-repeat: no-repeat;
	background-position : center left 5px;
	background-size: 25px;
}

/* 버튼은 가상 클래스를 가질 수 있다 */
.login button {
	width: 100%;
	border: none;
	padding: 5px;
	margin: 5px 0;
}

.login input[type=text] {
	background-image: url(images/icon-user.png);
	background-size: 22px;
}

.login input[type=email] {
	background-image: url(images/icon-email.png);
	background-size: 20px;
}

.login input[type=password] {
	background-image: url(images/icon-password.png);
	background-size: 20px;
}

.login label {
	display: block;
	text-align: center;
}
.login label input[type=checkbox],
.login label input[type=radio] {
	
}
```

## 다양한 속성 선택자 활용하기

선택자[속성이름~=”속성값”] : 속성 값으로 시작하는 요소 선택

선택자[속성이름|=”속성값”] : 속성 값 또는 - 으로 연결된 속성 값만 선택

선택자[속성이름^=”속성값”] : 속성 값으로 시작하는 요소 선택

선택자[속성이름$=”속성값”] : 속성 값으로 끝나는 요소 선택

!!중요!! 선택자[속성이름*=”속성값”] : 시작 끝 관계없이 속성 값이 포함된 요소 선택

ex: class=”text-center”