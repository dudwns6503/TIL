# HTML + CSS

## float 속성 1 (가로 배치하기, float 속성 상속)

!! HTML 엘리먼트는 기본이 왼쪽 정렬(float: none이 기본이다)

!! float 속성이 적용이 되면 모든 요소의 디스플레이 속성 inline-block 이 된다.

```css
/* HTML
<div class="parent">
	<div class="child"></div>
	<div class="child"></div>
	<div class="child"></div>
</div>
*/

/* 부모의 border 때문에 가로로 한 번에 안 담긴다. */
.parent {
	border: 5px solid #000;
	width: 600px;
	box-sizing: content-box;
}

/* float 속성을 주는 순간 가로로 배치됨 & 부모 요소도 높이를 잃어버림 */
.child {
	border: 5px solid red;
	width: 200px;
	height: 200px;
	float: left;
}
```

### float된 요소와 인접한 요소의 float 속성 상속

```css
/* HTML
<div class="frame">
  <img src="asdfd">
  <p>
    asdfadfadf
  </p>
</div>
*/

.frame {
	border: 1px solid #000;
	width: 800px;
}

.frame img {
	float: left;
}

.frame p {
	clear: both;
}
```

## float 속성 2(부모 요소의 높이 값 찾기, calc 함수로 사칙 연산)

```css
/* 한 줄에 2개의 요소를 각각 왼쪽 오른쪽으로 배치하기 */
/* HTML
<header>
  <nav>
    <div class="logo">Logo</div>
    <div class="menu">Navigation</div>
  </nav>
</header>
*/

header {
	background-color : #ccc;
	padding: 20px;
}
header nav {
	background-color: pink;
	width: 900px;
	margin: auto;
}
header nav div {
  width: 200px;
  height: 50px;
  background-color: yellowgreen;
}
/* 마지막에 끝내는 아이디 or 클래스라면 부모요소 생략하는 것이 좋음 */
/* 이렇게 설정한 순간 배경이 핑크인 애가(nav) 안보임 */
.logo {
	float: left;
}
.menu {
	float: right;
}
```

### 부모요소 높이 값 찾기

```css
/* HTML
	<section class="portfolio">
	  <div class="items>
	    <div class="item">item #01</div>
	    <div class="item">item #02</div>
	    <div class="item">item #03</div>
	    <div class="item">item #04</div>
	  </div> 
	</section>
*/

/* float 속성을 추가하는 순간 portfolio와 items의 높이 값을 잃어버림 */
.portfolio {
	background-color: #ddd;
	padding: 15px;
}
.items {
	background-color: yellowgreen;
	width: 1200px;
	margin: auto;
	box-sizing: content-box /* 이 부분을 추가해야 items를 확인할 수 있음 */
}
.item {
	border: 5px solid red;
	width: 300px;
	height: 300px;
	float: left;
}
```

### 높이를 찾는 방법

1. 위 예제에서 4개 중에서 1, 2, 3번만 float: left 한다.
2. 위 예제에서 items의 높이를 강제로 준다. height: 300px;
3. items에 overflow: hidden 한다.
4. 가상 클래스 이용

```css
.items:after {
	content: '';
	display: block;
	clear: both;
}
```

### calc 함수로 사칙연산

```css
.items {
	background-color: yellowgreen;
	width: 1280px;
	margin: auto;
	border: 5px solid #000;
	box-sizing: content-box
	overflow: hidden;
}
.item {
	border: 5px solid red;
	float: left;
	height: 300px;
	width: calc(1280px / 4); /* div의 갯수만큼 나눠줌*/
}
```

### float로 변경된 inline-block과 기본적인 inline-block의 차이

inline-block : 기본적으로 자신이 가지고 있는 컨텐츠 만큼 너비가 설정이됨. + 너비를 설정할 수 있음(block 성질)

float : float으로 만들어진 inline-block은 마진이 안 생긴다.