# BEM

### 20210426

### 개요

클래스 명을 정하는 작성하는 다양한 방법 중 BEM 이라는 방식이

현재 내가 사용하고 있는 방식과 유사하여서, 규칙을 지키면서 작업하면 좋겠다는 생각이 들어 기록한다. 

클래스 명을 정의할 때 '이것이 정답이다.' 는 없지만 다른 사람과 코드를 주고 받거나

시간이 흐르고 내가 작성한 코드를 확인할 때 등 __유지보수__ 를 위해서 필요한 부분이다.

B - Block

E - Element

M - Modifier

세가지 타입으로 나누어서 작성하는 것으로

소문자와 숫자만 사용하며, 작성은 아래와 같은 방식.
```html
class="block__element—modifier"
```

### Block

- 기능적으로 독립된 구성요소

    (* 각각 개별적으로 사용할 수 있는 형태)

- 형태나 상태가 아닌 목적이나 기능에 맞게 작성한다.
- 합성어는 '-' 으로 구분하여 작성한다.
```html
class="block"
class="sub-block"
```

### Elements

- 블록 안에서 특정 기능을 담당하는 부분
- 형태나 상태가 아닌 목적이나 기능에 맞게 작성한다.
```html
class="block__element"
```

### Modifier

- 블록이나 요소의 형태나 상태를 정의
- 수식어는 단독으로 사용하지 않고, 블록과 요소에 추가하여 사용한다.
```html
class="block--modifier"
class="block__element--modifier"
```

### 예시
##### Before

```html
<div class="main-contents" id="main-contents">
  <div class="main-contents-box">
    <a class="main-contents-img" href="static/works/work1.html">
    <img src="http://lorempixel.com/700/1800/" alt="work img"></a>
    <div class="main-contents-text-leftalign">
      <h3 class="main-contents-number pinkcolor">01.</h3>
      <h2 class="main-contents-title en">Works Title</h2>
      <h2 class="main-contents-title ko">작품 이름</h2>
     </div>
  </div>
  <div class="main-contents-box">
    <a class="main-contents-img" href="static/works/work1.html">
    <img src="http://lorempixel.com/700/1800/" alt="work img"></a>
    <div class="main-contents-text-rightalign">
      <h3 class="main-contents-number pinkcolor">01.</h3>
      <h2 class="main-contents-title en">Works Title</h2>
      <h2 class="main-contents-title ko">작품 이름</h2>
     </div>
  </div>
</div>
```

##### After

```html
<div class="main-contents" id="main-contents">
  <div class="main-content">
    <a class="main-content__img" href="static/works/work1.html">
    <img src="http://lorempixel.com/700/1800/" alt="work img"></a>
    <div class="main-content-text-box--left-align">
      <h3 class="main-content-text-box__number pinkcolor">01.</h3>
      <h2 class="main-content-text-box__title en">Works Title</h2>
      <h2 class="main-content-text-box__title ko">작품 이름</h2>
     </div>
  </div>
  <div class="main-content">
    <a class="main-content__img" href="static/works/work1.html">
    <img src="http://lorempixel.com/700/1800/" alt="work img"></a>
    <div class="main-content-text-box--right-align">
      <h3 class="main-content-text-box__number pinkcolor">01.</h3>
      <h2 class="main-content-text-box__title en">Works Title</h2>
      <h2 class="main-content-text-box__title ko">작품 이름</h2>
     </div>
  </div>
</div>
```
``Block``의 집합은 복수형으로 작성하여 묶었다. 
```html
<div class="main-contents" id="main-contents">
```
  
``Element`` 의 깊이는 2단계가 되지 않도록 ``Block`` 이름을 재정의한다.
```html
<div class="main-content-text-box--left-align">
<div class="main-content-text-box--right-align">
```

전반적으로 수정했을 때 ``class`` 의 이름이 길어지는 경향이 있는 것 같지만,

가령 1000~ 10000 줄 이상의 코드의 유지보수를 생각한다면 길어도 찾기 쉬운 것이 맞지 않을까?
