languege-switch-button
=======

### 20210424

웹사이트에서 언어 변경 버튼을 만들 때 사용한 ``javascript`` 를 기록한 내용이다.

### 개요

``html`` 태그에서 특정 문자열, class 등을 찾아서 해당하는 항목을 __보이게 만들고, 보이지 않게 만듦__ 으로서 해당 기능을 수행할 수 있다.

변경하고 싶은 언어로 된 내용을 ``html`` 태그에 __모두__ 입력해야 한다.

```html
ex)
<h1 class="ko">안녕하세요.</h1>
<h1 class="en">Hello.</h1>
...etc
```

특정 버튼을 눌렀을 때, 해당 기능을 수행하기 위해서는 ``.addEventListener("click", function, boolean);`` 를 이용한다.

##### html

변경하고자 하는 내용들에 class를 부여했다.
```html
//영어
<h2 class="en">Hi, guys. 😁<br>
I'm Daekyo Jeong. <br>
thx u for visiting my website. 🙏 <br><br>
I based in Seoul. 🇰🇷<br> I studied interaction design. 🎨<br>
I dream of becoming a developer. 🧑‍💻<br>
Thx u.
<br><br>
</h2>
//한국어
<h2 class="ko">안녕하세요. 😁<br>
저는 정대교입니다. <br>
제 웹사이트에 방문해주셔서 감사합니다. 🙏 <br><br>
서울에 거주중입니다. 🇰🇷<br>인터랙션 디자인을 공부했습니다. 🎨<br>
개발자가 되는 것을 꿈꾸고 있습니다. 🧑‍💻<br>
감사합니다.
<br><br>
</h2>
```

##### javascript
```javascript
//함수의 시작
function toggleLanguege(event) {
//ko, en 이라는 클래스를 포함한 모든 태그 선택
    var LanguegeKo = document.getElementsByClassName("ko");
    var LanguegeEn = document.getElementsByClassName("en");

//클래스는 배열로 이뤄져 있어서 for문을 이용하여서 개체를 제어할 수 있다.
    switch (event.target.id) {
        case 'korean':
            for (var i = 0; i < LanguegeKo.length; i++) {
                var item = LanguegeKo.item(i);
                var item2 = LanguegeEn.item(i);
                item.style.display = "block";
                item2.style.display = "none";
            }

            break;
        case 'english':
            for (var i = 0; i < LanguegeKo.length; i++) {
                var item = LanguegeKo.item(i);
                var item2 = LanguegeEn.item(i);
                item.style.display = "none";
                item2.style.display = "block";
            }

            break;
//default를 설정했지만, 전혀 효과가 없었다.
//내 생각에는 default는 case의 조건에 해당하지 않는 값이 입력되었을 때 작동하는 것으로 판단된다.
        default:
            for (var i = 0; i < LanguegeKo.length; i++) {
                var item = LanguegeKo.item(i);
                var item2 = LanguegeEn.item(i);
                item.style.display = "none";
                item2.style.display = "block";
            }
    }
```
   
같은 내용이지만 if문으로 작성한 방법

```javascript
    //    if (event === "korean") {
    //        for (var i = 0; i < LanguegeKo.length; i++) {
    //            var item = LanguegeKo.item(i);
    //            var item2 = LanguegeEn.item(i);
    //            item.style.display = "block";
    //            item2.style.display = "none";
    //
    //        }
    //        console.log(event);
    //    }
    //    if (event === "english") {
    //        for (var i = 0; i < LanguegeKo.length; i++) {
    //            var item = LanguegeKo.item(i);
    //            var item2 = LanguegeEn.item(i);
    //            item.style.display = "none";
    //            item2.style.display = "block";
    //        }
    //        console.log(event);
    //    }
}
```

##### html

버튼으로 지정할 태그를 선택하고 그것에 이벤트를 부여한다.

```html
<div class="footer-languege">
  <p id="korean">한국어</p>
  <p id="english">English</p>
</div>
```

지금보니 버튼의 id를 좀 더 직관적으로 변경해야할 듯.

```javascript
//let, var, const 변수에 대한 내용을 다시한번 배워야할 듯
//한국어, 영어로 변경할 버튼을 지정
let translatetoKo = document.getElementById("korean");
let translatetoEn = document.getElementById("english");

//addEventListener를 이용해 버튼이 아닌 것들을 버튼으로 만들어주는 과정
//"click"은, hover, change 등 다른 이벤트 상황을 사용할 수 있다.
translatetoKo.addEventListener("click", toggleLanguege, false);
translatetoEn.addEventListener("click", toggleLanguege, false);
```

이런식으로 해당 페이지 내에서만 작동하는 언어 스위치 버튼을 만들었다.

``javascript``에 추가적인 기능을 포함하면 다른 페이지로 이동하였을 때도 

처음 선택한 언어가 default 값이 될 수 있도록 조정이 가능할 것으로 판단된다.

> document.querySelectorAll 로 가능할 것 같은데, 도무지 방법을 못 찾아서 쩔쩔 메다가 class로 해결했다.
