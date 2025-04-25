# HTML + CSS

## CSS 가상클래스의 모든 것

### hover 가상 클래스 01(a태그 상태 가상 클래스, 버튼 디자인)

a:link → 링크 방문하기 전

a:visited → 링크 방문한 후

a:hover → 링크에 마우스 올렸을 때

a:active → 링크 클릭하고 마우스를 떼지 않은 상태

::placeholder ⇒ css3부터 생긴 가상클래스는 세미콜론을 두 개 사용해야 한다.

```css
/* HTML
<div class="frame">
  <a href="#none" target="_blank">링크 방문하기 전</a>
  <a href="http://www.inflearn.com" target="_blank">링크 방문한 후</a>
  <a href="#none" target="_blank">링크에 마우스 올렸을 때</a>
  <a href="#none" target="_blank">링크 클릭하고 마우스를 떼지 않은 상태</a>
</div>
*/

body {
  margin: 50px;
  line-height: 1.6em;
}

.frame a {
  text-decoration: none;
  display: block;
}

.frame a:hover {
  color: blue;
}

.frame a:active {
  color: red;
}
```

버튼

```css
/* HTML 
<div class="frame">
  <a href="#none" class="btn">normal link</a>
  <a href="#none" class="btn success">confirm link</a>
  <a href="#none" class="btn warning">warning link</a>
  <a href="#none" class="btn error">error link</a>
  <a href="#none" class="btn critical-error">critical-error link</a>
</div>
*/

body {
  line-height: 1.6em;
  margin: 50px;
}

.btn {
  text-decoration: none;
  padding: 5px 10px;
  border-radius: 5px;
  text-transform: capitalize;
  color: #fff;
  background-color: #00a8ff;
  width: 150px;
  display: inline-block;
  text-align: center;
  transition: 0.3s;
}

/* transition은 hover가 아닌 곳에 주어야 함. 마우스가 올라갈 때는
   적용되지만 아닐 때는 적용이 안됨*/
.btn:hover {
  opacity: 0.7;
}

.success {
  background-color: #4cd137;
}
.warning {
  background-color: #fbc531;
}
.error {
  background-color: #ee5a24;
}
.critical-error {
  background-color: #ea2027;
}

```

translate 속성은 중첩해서 사용하지 말 것

.download:hover i ⇒ download에 호버했을 때 i를 바꾸고 싶은 경우

transform 속성은 inline에는 적용되지 않는다. inline-block or block에 적용해야 함.

### hover 가상 클래스 02(hover로 만드는 버튼 디자인, 드롭다운 내비게이션 & 컨텐츠)

```css
/* HTML 
<div class="dropdown">
  <button class="dropdown-btn">Real Estate Type</button>
  <div class="dropdown-content">
    <a href="none">All</a>
    <a href="none">One room</a>
    <a href="none">1.5 rooms</a>
    <a href="none">Two room</a>
    <a href="none">Three</a>
    <a href="none">Officetel</a>
    <a href="none">Apartment</a>
  </div>
</div>
*/

.dropdown {
  width: 200px;
}
.dropdown:hover .dropdown-content {
  display: block;
}
/* inherit 사용해서 부모 요소의 너비를 상속함 */
.dropdown-btn {
  width: inherit;
  background-color: #3e8e41;
  color: #fff;
  padding: 7px;
  border: none;
}
.dropdown-content {
  display: none;
  box-shadow: 0 0 5px lightgray;
}
.dropdown-content a {
  display: block;
  color: #000;
  text-decoration: none;
  text-align: center;
  padding: 5px;
}
.dropdown-content a:hover {
  background-color: #f1f1f1;
}
```

IMG 같은 경우 상위요소의 너비를 받기 위해서 width: 100% 해주는 것이 좋다.

IMG 같은 경우 inline-block 인데 display: block으로 바꿔주면 기존에 가지고 있는 아래 마진을 없앨 수 있다.

display: none → block 은 transition을 적용할 수 없음. 따라서 transition을 적용하려면 opacity를 통해서 나타낸다.

opacity를 썼을 때 단점은 보이지 않는 상태에서도 자리를 차지한다는 것이다. 부모와 자식간의 position을 설정한 후, 위치를 조정해주면 된다.