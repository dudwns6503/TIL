# HTML + CSS

## 순서를 체크하는 가상 클래스

### nth-child, first-child, last-child

```css
/* HTML
<div>
  <h2>첫번째 헤드라인 요소</h2>
  <h2>두번째 헤드라인 요소</h2>
  <p>
    Lorem, ipsum dolor sit amet consectetur adipisicing elit. Harum veniam
    minus facilis. Modi eveniet distinctio nulla totam dolores corrupti!
    Laboriosam doloremque exercitationem adipisci qui nobis amet dolor vitae
    ipsa voluptatum?
  </p>
  <h2>세번째 헤드라인 요소</h2>
</div>
*/

/* 중간에 p가 있으면 생각했던 대로 적용이 안 되는 문제가 생길 수 있다.*/
div h2:nth-child(1) {
  color: red;
}
div h2:nth-child(2) {
  color: blue;
}
div h2:nth-child(3) {
  color: limegreen;
}

```

nth-child(odd) : 홀수만 적용

nth-child(even) : 짝수만 적용

```css
/* HTML
<table class="employee">
  <caption>
    Employee of the Month
  </caption>
  <tr>
    <th>Name</th>
    <th>Email</th>
    <th>Phone</th>
  </tr>
  <tr>
    <td>Francis C. Albers</td>
    <td>example@example.com</td>
    <td>123-45-678</td>
  </tr>
  <tr>
    <td>Ronnie S. Crews</td>
    <td>example@example.com</td>
    <td>123-45-678</td>
  </tr>
  <tr>
    <td>John B. Richards</td>
    <td>example@example.com</td>
    <td>123-45-678</td>
  </tr>
  <tr>
    <td>Debbie S. Khan</td>
    <td>example@example.com</td>
    <td>123-45-678</td>
  </tr>
</table>
*/

.employee {
  width: 700px;
  border-collapse: collapse;
  table-layout: fixed;
}
.employee td,
.employee th {
  /* border: 1px solid #ccc; */
  padding: 5px;
  text-align: center;
}
.employee th {
  background-color: limegreen;
  color: #fff;
}
.employee tr {
  border-bottom: 1px solid #ccc;
}
.employee tr:hover {
  background-color: #eee;
}
/* stripe 디자인 */
/* .employee tr:nth-child(odd) {
  background-color: #eee;
} */
.employee tr:first-child {
  border: none;
}
.employee tr:last-child {
  border: none;
}
.employee caption {
  font-size: 32px;
  margin-bottom: 25px;
}
.employee tr td:first-child {
  font-weight: bold;
}
.employee tr td:last-child {
  color: royalblue;
}
```

### nth-child, nth-of-type, 기타 순서체크 가상 클래스

nth-child

```css
/* HTML 
<div class="items">
  <div class="item">
    <h3>Item Headline #01</h3>
    <p>
      Lorem ipsum dolor sit amet consectetur adipisicing elit. Est doloribus
      ipsa perspiciatis consectetur doloremque molestiae maxime temporibus
      eligendi minima, ducimus nobis eum, numquam libero id error. Impedit
      dicta architecto nihil?
    </p>
    <a href="#none">read more</a>
  </div>
  <div class="item">
    <h3>Item Headline #02</h3>
    <p>
      Lorem ipsum dolor sit amet consectetur adipisicing elit. Est doloribus
      ipsa perspiciatis consectetur doloremque molestiae maxime temporibus
      eligendi minima, ducimus nobis eum, numquam libero id error. Impedit
      dicta architecto nihil?
    </p>
    <a href="#none">read more</a>
  </div>
  <div class="item">
    <h3>Item Headline #03</h3>
    <p>
      Lorem ipsum dolor sit amet consectetur adipisicing elit. Est doloribus
      ipsa perspiciatis consectetur doloremque molestiae maxime temporibus
      eligendi minima, ducimus nobis eum, numquam libero id error. Impedit
      dicta architecto nihil?
    </p>
    <a href="#none">read more</a>
  </div>
</div>
*/

.items {
  display: flex;
  gap: 10px;
}
.item {
  border: 1px solid #000;
  padding: 15px;
}
.item a {
  text-decoration: none;
  text-transform: capitalize;
  color: #000;
  padding: 5px;
  display: block;
  text-align: center;
  border-radius: 3px;
  color: #fff;
}

/* .item a:nth-child(1) 이런 식으로 선택하면 안 된다. */
.item:nth-child(1) a {
  background-color: limegreen;
}
.item:nth-child(2) a {
  background-color: crimson;
}
.item:nth-child(3) a {
  background-color: royalblue;
}
```

nth-of-type

```css
/* HTML 
<div class="frame">
  <h1>Text in div1</h1>
  <p>Text in p1</p>
  <p>Text in p2</p>
  <p>Text in p3</p>
  <p>Text in p4</p>
</div>
*/

/* nth-child(1)로 했을 때 p가 아닌 애가 맨 위에 있을 경우 
   적용이 안 될 수가 있음 */
.frame p:nth-of-type(1) {
  color: crimson;
}
```

## 실전 예제

```css
/* HTML 
<div class="profile">
  <img class="face" src="images/face.jpg" />
  <h2>Kathey A. Threlkeld</h2>
  <ul>
    <li><span>Birthday</span> July 20, 1992</li>
    <li><span>Age</span> 29 years old</li>
    <li><span>Email</span> leland90@tyonyihi.com</li>
    <li><span>Phone</span> (291)330-6297</li>
    <li><span>Occupation</span> UI/UX designer</li>
    <li><span>Address</span> 1227 Platinum Drive Pittsburgh, USA</li>
  </ul>
  <div class="content">
    <p>
      <b>What I do</b>
      I worked at a web agency as a UI/UX designer for about 7 years and as
      a <em>front-end publisher</em> for the last 7 years. As a front-end
      publisher, I published various coding websites made with
      <em>variable skills.</em>
    </p>
    <a href="#none">contact me</a>
  </div>
  <div class="content">
    <p>I look forward to new projects with good people. thank you.</p>
  </div>
</div>
*/

@import url("https://fonts.googleapis.com/css2?family=Montserrat:ital,wght@0,100..900;1,100..900&family=Open+Sans:ital,wght@0,300..800;1,300..800&display=swap");
@import url("https://fonts.googleapis.com/css2?family=Playfair:ital,wght@0,100..900;1,100..900&family=Open+Sans:ital,wght@0,300..800;1,300..800&family=Playfair:ital,opsz,wght@0,5..1200,300..900;1,5..1200,300..900&display=swap");
* {
  box-sizing: border-box;
}

body {
  font-family: "Monteserrat", "Playfair Display";
  font-size: 15px;
  line-height: 1.6em;
  letter-spacing: -1px;
  background-image: linear-gradient(120deg, #a1c4fd 0%, #c2e9fb 100%);
  height: 100vh;
  margin: 0;
}

.profile {
  width: 400px;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  padding: 30px;
  border-radius: 15px;
  background-color: #fff;
  box-shadow: 0 0 15px rgba(0, 0, 0, 0.1);
  padding-top: 80px;
}
.profile .face {
  border-radius: 50%;
  width: 150px;
  height: 150px;
  border: 5px solid #eee;
  position: absolute;
  left: 50%;
  transform: translateX(-50%);
  top: -75px;
}
.profile h2 {
  text-align: center;
  font-weight: 500;
}
.profile ul {
  list-style: none;
  padding: 0;
}
.profile ul li {
  border-bottom: 1px solid #ddd;
  padding: 5px 0px;
}
.profile ul li span {
  font-weight: 500;
  width: 90px;
  display: inline-block;
}
.profile .content:nth-of-type(1) p b {
  font-size: 18px;
  display: block;
}
.profile .content:nth-of-type(1) a {
  background-color: royalblue;
  color: #fff;
  font-size: 1.2em;
  text-decoration: none;
  padding: 5px;
  text-transform: capitalize;
  display: block;
  text-align: center;
  transition: 0.35s;
}

.profile .content:nth-of-type(1) a:hover {
  background-color: #000;
}

.profile .content:nth-of-type(1) p em {
  font-style: normal;
  text-decoration-line: underline;
  text-decoration-style: dotted;
  text-decoration-color: crimson;
  text-underline-offset: 3px;
}

.profile .content:nth-of-type(2) p {
  font-family: "Playfair Display", "serif";
  font-size: 1.2em;
  text-align: center;
}
```