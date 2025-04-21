# HTML + CSS

## 포지션 속성 1(static, relative, absolute, fixed, sticky)

알아두어야할 것

- 부모 요소 relative, 자식 요소 absolute
- 포지션 속성의 기본 값은 position : static
- 포지션 속성이 없으면 left, right, top, bottom, z-index 사용할 수 없음. 곧, 포지션 속성과 반드시 같이 사용(static 제외)

static : position 속성이 없음

absolute : 요소가 절대적인 위치에 배치

relative : 요소가 상대적인 위치에 배치

fixed : 최초의 좌표에 고정됨

sticky : 스크롤 된 후 좌표로 고정됨

```css
    /* HTML
    <div class="items">
      <div class="item1">items1</div>
      <div class="item2">items2</div>
      <div class="item3">items3</div>
    </div>
    */
    
.items div {
  border: 1px solid #000;
  width: 200px;
  height: 200px;
}

.item1 {
  position: static;
}
/* 부모 요소 관계를 맺을 때, 좌표, z-index를 사용해야 하는 경우에 주로 쓰임 */
/* 보통 아래와 같이 relative로 위치를 지정하는 경우는 많지 않다 */
.item2 {
  background-color: yellowgreen;
  position: relative;
  top: 100px;
  left: 100px;
}
/* 다른 요소에 관계 없이 자기가 가고 싶은 곳으로 감 */
.item3 {
  background-color: crimson;
  position: absolute;
  top: 0;
  right: 0;
}
```

```css
/* HTML
    <div class="box"></div>
*/

/* HTML 요소는 위치를 왼쪽 상단을 기준으로 계산한다 */
.box {
  width: 100px;
  height: 100px;
  background-color: crimson;
  position: absolute;
  top: 0;
  left: 50%;
  transform: translateX(-50%);
}

/* 가운데로 보내기 위해서 transform 또는 translate를 사용한다*/
.box {
  width: 100px;
  height: 100px;
  background-color: crimson;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
```

## 부모 요소 자식 요소 관계 만들기

```css
/* HTML
    <div class="parent">
      <div class="child"></div>
    </div>
*/

:root {
  --size: 150px;
}

/* absolute는 position: static 속성을 가지고 있지 않은 조상을 기준으로 작동한다. */
body {
  margin: 100px;
}

.parent {
  width: 600px;
  height: 400px;
  border: 5px solid #000;
  position: relative;
}

.child {
  width: var(--size);
  height: var(--size);
  border-radius: 50%;
  background-color: crimson;
  position: absolute;
  top: calc(var(--size) / -2);
  left: 50%;
  transform: translateX(-50%);
}

```

## absolute, fixed, sticky 차이점

```css
/* HTML
    <header>
      <div class="banner">This is banner area.</div>
      <nav>This is Navigation</nav>
    </header>

    <a class="gototop" href="#none">Go to top</a>
*/

body {
  margin: 0;
  height: 200vh;
}

/* position을 주자마자 너비가 줄어든다. why?
   모든 요소는 position :absolute 또는 fixed를 주게 되면 inline-block으로 변경된다. */
header {
  height: 200vh;
}

header .banner {
  height: 100px;
  background-color: yellowgreen;
}

header nav {
  height: 100px;
  background-color: crimson;
  position: sticky;
  top: 0;
}

.gototop {
  position: fixed;
  right: 20px;
  bottom: 20px;
}
```

## 부모요소 내부와 외부에서 자유롭게 배치하기

에밋으로 한 번에 만들기

- .outside$*8{inside$}
- .parent>.inside$*8

.parent div[class*=outside]

left: 0 은 right 100% 이다.

## 포지션 속성 우선순위

- z-index 같다는 기준으로 relative > absolute
- z-index 같다는 기준으로 2개의 absolute가 있으면 html 순서가 나중인 것이 우선

```css
/* HTML
<div class="box1">box1</div>
<div class="box2">box2</div>
<div class="box3">box3</div>
*/

div[class*="box"] {
  width: 200px;
  height: 200px;
  font-size: 2em;
  text-align: center;
  line-height: 200px;
  position: absolute; /* position을 주면 기본적인 z-index(0)가 들어간다. */
}

.box1 {
  background-color: crimson;
  top: 0;
  left: 0;
}
.box2 {
  background-color: royalblue;
  top: 50px;
  left: 50px;
}
.box3 {
  background-color: yellowgreen;
  top: 100px;
  left: 100px;
}
```

z-index 같다는 기준으로 relative > absolute  예시

```css
/* HTML
<div class="card">
  <h2>Card Headline</h2>
  <p>
    Lorem ipsum dolor, sit amet consectetur adipisicing elit. Esse, culpa
    veniam? Hic, doloremque est nisi, asperiores doloribus ut ad officia,
    veritatis ullam voluptates vel tempora quam dicta vero expedita libero
    reiciendis et modi! Minus autem reprehenderit nemo illo a totam illum
    praesentium, quasi magnam voluptatem sit. Error perferendis quod sequi.
  </p>
  <a href="none">Read More</a>
</div>
*/

.card {
  border: 1px solid #000;
  padding: 20px;
  border-radius: 10px;
  width: 400px;
  overflow: hidden;
  position: relative;
}
.card:before {
  content: "";
  width: 100%;
  height: 100%;
  background-color: rgba(65, 105, 225, 0.3);
  position: absolute;
  top: 0;
  left: 0;
}

.card h2 {
  margin-top: 0;
}

.card p {
}

.card a {
  float: right;
  text-decoration: none;
  text-transform: uppercase;
  color: #fff;
  background-color: crimson;
  padding: 5px;
  border-radius: 5px;
  position: relative; /* relative를 설정함으로써 before보다 우선순위up 클릭할 수 있게 됨 */
}
```

## Display 속성 1(inline, inline-block, block 4가지 특징)

1. 기본 너비 값
2. 한 줄에 하나 or 여러개
3. width를 가질 수 있는가?
4. margin을 가질 수 있는가?

## Display 속성을 활용해 HTML 구조 쉽게 만들기
```css
/* HTML
    <!-- border를 정교하게 사용할 경우 아래와 같이 작성하는 것이 좋음 -->
    <ul>
      <li><a href="#none">navigation #01</a></li>
      <li><a href="#none">navigation #02</a></li>
      <li><a href="#none">navigation #03</a></li>
      <li><a href="#none">navigation #04</a></li>
    </ul>

    <hr style="margin: 50px; clear: both" />

    <!-- border 정교하게 안해도 될 경우 아래와 같이 작성해도 됨 -->
    <div>
      <a href="#none">navigation #01</a>
      <a href="#none">navigation #02</a>
      <a href="#none">navigation #03</a>
      <a href="#none">navigation #04</a>
    </div>
*/

a {
  text-decoration: none;
  color: #000;
}

ul {
  margin: 0;
  padding: 0;
  list-style: none;
  overflow: hidden;
}

ul li {
  border: 1px solid #000;
  float: left;
  width: 150px;
  text-align: center;
  padding: 5px;
}

div {
}

div a {
  border: 1px solid #000;
  width: 150px;
  display: inline-block; /* 기본 마진이 생김 */
  text-align: center;
  padding: 5px;
}
```