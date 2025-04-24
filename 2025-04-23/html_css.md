# HTML + CSS

## Box Model 속성 01(width, height, inherit, auto)

- 기본 너비(width)는 display 속성에 따라 다름
- 기본 높이(height)는 auto

### calc 및 변수를 활용하여 너비 쉽게 변경하고 계산하기

```css
/* HTML
<div class="frame">
  <div class="item item1">item #01</div>
  <div class="item item2">item #02</div>
  <div class="item item3">item #03</div>
</div>
*/

a {
  text-decoration: none;
  color: #000;
}

.frame {
  width: var(--width);
  overflow: hidden;
}

.frame .item {
  border: 5px solid red;
  height: 300px;
  float: left;
  width: calc(var(--width) / 3);
}

:root {
  --width: 800px;
}
```

### 반응형 웹에서 height: auto 사용하기

```css
    /* HTML
    <div class="container">
      <section class="about">
        <h1>Section : About</h1>
        <div class="inner">
          <div>
            Lorem ipsum dolor sit, amet consectetur adipisicing elit. Ab,
            corrupti, alias libero, perferendis veritatis dolores officia
            adipisci quidem praesentium asperiores cum quos sapiente dicta iusto
            error ad mollitia architecto ducimus laboriosam enim reprehenderit
            maiores. Earum ex dolores, veritatis voluptatem cupiditate, id est
            eaque, quod perspiciatis fugit nulla temporibus magnam hic!
          </div>
          <div>
            Lorem ipsum, dolor sit amet consectetur adipisicing elit. Corporis
            quas incidunt debitis in harum eius vel, quibusdam deserunt tenetur
            ad, dolorum, adipisci exercitationem quia unde quo voluptas deleniti
            dolores. Voluptatem quisquam nesciunt veritatis iure, earum,
            reprehenderit temporibus corrupti officia quasi, fuga ab cum soluta
            minima aperiam mollitia vel impedit ipsa ea velit illo! Animi,
            corrupti ea placeat magni porro et!
          </div>
        </div>
      </section>
    </div>
    */
    
body {
  margin: 0;
}

.container {
}

.about {
  border: 1px solid #000;
}

.about h1 {
  text-align: center;
}

.inner {
  border: 1px solid red;
  width: 1000px;
  margin: auto;
  overflow: hidden;
}

.inner div {
  border: 1px solid blue;
  float: left;
  width: 50%;
  height: 300px;
}

@media (max-width: 768px) {
  .about {
    background-color: #ddd;
  }

  .inner {
    width: 100%;
  }

  /* pc 버전에서 고정했던 너비와 높이를 모바일 버전에서 100%와 
     height: auto를 통해서 해제해줌 
  */
  .inner div {
    float: none;
    width: 100%;
    height: auto;
  }
}
```

### width, height, inherit, :before, :after

```css
/* HTML
<div class="profile">
  <div class="photo"></div>
  <p>
    Lorem ipsum dolor sit amet consectetur adipisicing elit. Tempore, itaque
    at eaque dolorem, consectetur, dignissimos consequuntur ipsam quaerat
    magni alias earum repellat ipsa? Ipsum optio doloremque ut minus, nam
    officiis modi deserunt rerum culpa explicabo recusandae excepturi et
    ullam libero?
  </p>
  <a href="#none">read more</a>
</div>
*/
    
a {
  text-decoration: none;
  color: #000;
}

:root {
  --width: 500px;
}

.profile {
  /* border: 1px solid #000; */
  width: 300px;
  margin: 50px auto;
  border-radius: 15px;
  padding: 15px;
  box-shadow: 0 0 20px rgba(0, 0, 0, 0.15);
  position: relative;
  overflow: hidden;
}

/* before, after는 inline요소이며 반드시 content를 설정해줘야 한다 */
/* inherit을 통해 .profile의 width를 그대로 받음 */
/* height 같은 경우 이 경우에는 부모가 height가 없기 때문에 
   0을 물려받아서 보이지 않게 된다.*/
.profile:before {
  content: "";
  width: inherit;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.2);
  position: absolute;
  left: 0;
  top: 0;
}

.photo {
  border: 1px solid #000;
  width: 100px;
  height: 100px;
  border-radius: 50%;
  margin: auto;
}

.profile a {
  text-transform: uppercase;
  background-color: yellowgreen;
  color: #fff;
  padding: 5px;
  display: block;
  text-align: center;
}

```

## Box Model 속성 02(box-sizing)

## Box Model 속성 03(margin, padding, 마진 겹침, 네거티브 마진)

마진 겹침 : 겹치는 마진 중 더 큰 값을 가진다.(상하만, 좌우 마진은 마진 겹침이 없다)

네거티브 마진 : 한 줄로 나란히 세울 때 마진을 없애기 위해서 - 마진을 주는 경우가 있음(잘 안씀)

```css
/* HTML
<div class="parent">
  <div class="child">child</div>
</div>
*/  

/* 
   parent에 width를 고정적으로 주는 것이 아니라 display:inline-block을 씀으로써
   child에 크기가 변해도 자동으로 조정된다 
*/
.parent {
  border: 1px solid #000;
  display: inline-block;
}

.child {
  background-color: crimson;
  width: 100px;
  height: 100px;
  margin: 30px;
}
```

## Box Model 속성 04(border, border-radius)

border-radius도 마찬가지로 상, 우, 하, 좌 순이다.

border 바깥에 있는 outline.

outline-offset을 -로 주게 되면 border 안쪽으로 보낼 수 있다.

## Table 스타일 속성

border-collapse : 표 테두리를 병합할지 또는 통합할지 여부 value : separate(기본 값) collapse

table-layout : 표의 너비와 일치하도록 셀의 너비를 균일하게 표시  value : auto(기본 값) fixed

caption-side : 캡션이 있는 테이블 제목 표시 value : top(기본 값) bottom

vertical-align: 표의 너비와 균일하도록 셀의 너비를 균일하게 표시 value: middle(기본 값) top bottom

empty-cell : 내용이 없는 빈 셀을 표시할지 여부 value: show(기본) hide

위의 3가지만 기억하면 됨

```css
/* HTML
<table class="crew">
  <caption>
    Crew List in 2021
  </caption>
  <tr>
    <th>#</th>
    <th>First</th>
    <th>Last</th>
    <th>Handle</th>
  </tr>
  <tr>
    <td>1</td>
    <td>Mark</td>
    <td>Otto</td>
    <td>@mdo</td>
  </tr>
  <tr>
    <td>2</td>
    <td>Jacob</td>
    <td>Thornton</td>
    <td>@fat</td>
  </tr>
  <tr>
    <td>3</td>
    <td>Larry</td>
    <td>the Bird</td>
    <td>@twitter</td>
  </tr>
</table>
*/

/* 테이블에 border-collapse, table-layout 을 사용해야 한다*/
.crew {
  border-collapse: collapse;
  width: 600px;
}
.crew td,
.crew th {
  text-align: center;
  padding: 5px;
}
.crew th {
  background-color: #222;
  color: #fff;
  border: none;
}
.crew tr {
  border-bottom: 1px solid #ddd;
}
.crew tr:last-child {
  border: none;
}

.crew caption {
  font-size: 26px;
  margin-bottom: 10px;
}
```