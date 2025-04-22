# HTML + CSS

## Display 속성 이해도가 없을 경우 생기는 비 웹표준 코딩

```css
/* HTML
<h1>
  고객들의 생생한 후기
  <span>고객들의 생생한 후기가 우리의 '심장'을 뛰게 합니다.</span>
</h1>

<div>
  <h1>
    고객들의 생생한 후기
    <span
      >고객들의 생생한 후기가 우리의 <em>'심장'</em>을 뛰게 합니다.</span
    >
  </h1>
</div>
*/  
    
a {
  text-decoration: none;
  color: #000;
}

h1 {
  font-weight: normal;
  font-size: 42px;
  text-align: center;
}

/* 웹 표준에 어긋나거나 br태그를 넣는게 아니라 display를 통해서 간단하게 줄바꿈을 할 수 있음*/
h1 span {
  display: block;
  font-size: 16px;
}

em {
  color: crimson;
  font-style: normal;
}

```

## 요소를 보이지 않게 하는 3가지 방법과 차이점

1. display: none (존재 X)

2. opacity : 0 (존재 O, 보이지 않게 함)

3. visiblity : hidden (자기 자리의 크기와 위치는 유지한채 사라짐)

2와 3의 차이점은? 

3번 같은 경우 cursor: pointer를 줬을 때 cursor가 작동하지 않음

```css
/* HTML
<div class="parent">
  <div class="child1">child1</div>
  <div class="child2">child2</div>
  <div class="child3">child3</div>
</div>
*/

parent div {
  border: 1px solid #000;
  width: 200px;
  height: 300px;
  display: inline-block;
  margin: 10px;
  text-align: center;
  line-height: 300px;
  font-size: 2em;
  cursor: pointer;
}

.parent div:nth-child(1) {
  background-color: skyblue;
}

.parent div:nth-child(2) {
  background-color: gold;
  /* display: none; */
  /* opacity: 0; */
  visibility: hidden;
}

.parent div:nth-child(3) {
  background-color: grey;
}

.parent div:hover {
  opacity: 1;
  visibility: visible;
}
```

## display 속성 완벽한 이해를 위한 필수 추가 사항

1. margin: auto로 요소를 중앙 정렬할 때 블록 요소만 가능.(인라인과 인라인 블록은 작동하지 않음)
2. 인라인 요소 또는 인라인 블록 요소를 중앙 정렬하려면 부모 요소에 text-align: center 속성을 사용
3. 모든 요소는 float 속성을 가지면 마진이 없는 인라인 블록으로 display 속성이 변경 된다.
4. 모든 요소는 position : absolute or fixed를 가지면 인라인 블록으로 display 속성이 바뀐다.
5. 인라인 요소의 display 속성을 block으로 변경하면 요소의 너비는 자동으로 100%로 변경된다. (인라인 블록 요소는 자동으로 100%가 되지 않으므로 직접 설정해야 함)
6. 가상 클래스 ::before, ::after의 최초 display 속성은 inline
7. block 요소의 기본 너비 값은 100% 이지만 table은 기본 너비값이 컨텐츠의 양만큼 너비가 자동으로 맞춰진다(너비를 가득 채우려면 width: 100%를 주어야 함)

## display 속성(list-item, table, flex와 grid, scss 활용 능력의 중요성)

### list-item

```css
/* HTML
<div class="display-list">
  <a href="#none">Premier League</a>
  <a href="#none">Serie A League</a>
  <a href="#none">Ligue 1 League</a>
  <a href="#none">Bundesliga League</a>
  <a href="#none">La Liga League</a>
</div>
*/

body {
  margin: 50px;
}

a {
  text-decoration: none;
  color: #000;
}

.display-list {
  border: 1px solid #000;
}

.display-list a {
  display: list-item;
  /* list-style-position: outside; */
  list-style-position: inside;
  list-style-type: circle; /* list-style을 쓰면 이상하게 outside가 됨 */
}
```

### table

```css
/* HTML
<ul>
  <li>item 1</li>
  <li>item 2</li>
  <li>item 3</li>
  <li>item 4</li>
  <li>item 5</li>
  <li>item 6</li>
  <li>item 7</li>
  <li>item 8</li>
</ul>
*/

a {
  text-decoration: none;
  color: #000;
}

ul {
  border: 1px solid red;
  list-style: none;
  padding: 0;
  margin: 0;
  display: table; /* 주는 순간 inline-block이 됨*/
  width: 100%;
  border-spacing: 15px;
}

ul li {
  display: table-cell;
  border: 1px solid #000;
  height: 150px;
  text-align: center;
  vertical-align: middle;
}

/* 두 줄을 만들고 싶은 경우 ul을 2개 만들어야 한다. */
```