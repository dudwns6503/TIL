# HTML + CSS

## Before After 가상 클래스

1. HTML 엘리먼트는 부모 요소, :before와 :after는 자식 요소
2. 가상 클래스 :before, :after는 인라인(inline) 요소
3. 크기 값을 주기 위해서는 블록 요소 또는 인라인 블록 요소로 변경해줘야 함
4. 가상 클래스 :before와 :after 사용할 때 반드시 content: ‘’; 가 있어야 함
5. :before와 :after를 position: absolute로 사용하는 경우 둘 중에 어떤 것을 사용해도 무관함
6. 모든 HTML 엘리먼트는 :before와 :after를 가질 수 있음(단 input, 폰트 아이콘은 가질 수 없다)

### 간단한 before, after

```css
/* HTML
<h1 class="headline">CodingWorks Publishing Online Class</h1>
*/

.headline:before {
  content: "♥";
  color: crimson;
  margin-right: 5px;
}
.headline:after {
  content: "#01";
  background-color: limegreen;
  color: #fff;
  font-size: 18px;
  margin-left: 5px;
  padding: 0 5px;
  border-radius: 3px;
  vertical-align: middle;
}
```

!! 폰트 사이즈는 기본 16px이다.

### HTML UniCode 및 세로 중앙 맞추기

```css
/* HTML 
<ul class="football">
  <li class="update">프리미어리그</li>
  <li>분데스리가</li>
  <li>라리가</li>
  <li>리그앙</li>
  <li>세리에</li>
</ul>
*/

.football {
  list-style: none;
  padding: 0;
}
.football li {
}
/* HTML Unicode */
.football li:before {
  content: "\26BD";
  font-size: 0.8em;
  transform: translateY(-1px); /* Vertical Align Middle로는 중앙 정렬이 어려움.*/
  display: inline-block;
}

```

### Badge 디자인

```css
/* HTML
<ul class="coffee">
  <li class="soldout">Nitro Cold Brew</li>
  <li>Caffeine Free</li>
  <li class="hit">Iced Coffee</li>
  <li class="hit">Specialty Coffee</li>
  <li>Brewed Coffee</li>
</ul>
*/

.coffee {
  list-style: none;
  padding: 0;
  /* li 사이 간격 */
  line-height: 1.6em;
}
.coffee li:before {
  content: "\2615";
  margin-right: 5px;
  font-size: 13px;
  transform: translateY(-1px);
  display: inline-block;
}
.coffee li.hit:after,
.coffee li.soldout:after {
  margin-left: 5px;
  text-transform: uppercase;
  font-size: 10px;
  transform: translateY(-1px);
  display: inline-block;
}
.coffee li.hit:after {
  content: "hit";
  color: crimson;
}
.coffee li.soldout:after {
  content: "soldout";
  color: royalblue;
}
.coffee li.soldout {
  color: #ccc;
  text-decoration: line-through;
}
```

### 포지션 활용(부모 요소, 자식 요소)

```css
/* HTML
<a href="#none" class="btn">
  <span>View the CodingWorks class</span>
</a>
*/

/* btn에 z-index를 넣더라도 :before, :after도 같이 z-index가 적용되기 때문에
   글씨가 계속 안 보이는 현상이 발생함 
*/
.btn {
  text-decoration: none;
  border: 1px solid #000;
  padding: 7px 15px;
  position: relative;
  transition: 0.35s;
  background-color: #000;
  color: #fff;
}
.btn:before {
  content: "";
  background-color: crimson;
  width: 100%;
  height: 0;
  position: absolute;
  bottom: 0;
  left: 0;
  transition: 0.35s;
  /* z-index: -1; */
}
/* span을 넣음으로써 z-index를 사용하지 않아도 hover할 때 글씨를 볼 수 있음 */
.btn span {
  position: relative;
}
.btn:hover:before {
  height: 100%;
}
```

```css
/* HTML
<div class="section-header">
  <h3>정말 쉽고 간단합니다.</h3>
  <h1>
    <span>카톡</span> 간편 회원 가입 후
    <b>카드매출 관리를 무료</b> 이용해보세요.
  </h1>
</div>
*/

.section-header {
  text-align: center;
}
.section-header h3 {
  color: #f37268;
  font-weight: 500;
  font-size: 25px;
}
.section-header h1 {
  font-weight: normal;
}
.section-header h1 span {
  position: relative;
}
.section-header h1 span:before {
  content: "";
  position: absolute;
  background-image: url(images/face.jpg) no-repeat;
  background-size: cover;
  width: 500px;
  height: 500px;
  top: -30px;
  right: -20px;
}
```

### 포지션 활용(Accordian Title Bullet)

```css
/* HTML
<div class="faq-title">What is Netflix?</div>
*/

@import url("//cdn.jsdelivr.net/npm/xeicon@2.3.3/xeicon.min.css");

.faq-title {
  background-color: #303030;
  color: #fff;
  padding: 10px;
  cursor: pointer;
  position: relative;
}
.faq-title:after {
  content: "\e9c5";
  font-family: xeicon;
  position: absolute;
  right: 10px;
  top: 50%;
  transform: translateY(-50%);
  transition: 0.35s;
}
/* translate 속성을 유지한 채로 해야함. 안그러면 덮어씌워짐 */
.faq-title.active:after {
  transform: translateY(-50%) rotate(45deg);
}
```