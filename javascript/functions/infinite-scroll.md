infinite-scroll
=======

### 20210428

웹사이트에서 무한스크롤을 구현할 때 사용한 ``javascript`` 를 기록한 내용이다.

자연스럽게 반복되는 스크롤을 구현하면서 겪은 문제와 해결방법에 대한 기록.

### 개요

``scrollTop`` 값을 이용하여 현재 ``scroll`` 위치를 파악하고, ``innerHTML`` 를 이용해

새로운 ``html`` 를 추가하여 ``scroll`` 끝 없이 이어지는 것 처럼 __착각__ 하게 만들 수 있다. 

스크롤의 움직임을 감지하여, 해당 기능을 수행하기 위해서는 ``.addEventListener("scroll", function, boolean);`` 를 이용한다.

##### html

스크롤 하고자 하는 ``.list`` 
```html
<div class="list">
  <ul class="list__content">
    <li class="list__content-title"><a href="">Breathe</a><img class="list__content-img" src="" alt=""></li>
    <li class="list__content-title"><a href="">Food a Cappella</a><img class="list__content-img" src="" alt=""></li>
    <li class="list__content-title"><a href="">LIMA Olympic</a><img class="list__content-img" src="" alt=""></li>
    <li class="list__content-title"><a href="">Universe</a><img class="list__content-img" src="" alt=""></li>
    <li class="list__content-title"><a href="">Neon</a><img class="list__content-img" src=""alt=""></li>
    <li class="list__content-title"><a href="">Salt Factory</a><img class="list__content-img" src="" alt=""></li>
    <li class="list__content-title"><a href="">Moonecklace</a><img class="list__content-img" src="" alt=""></li>
  </ul>
</div>
```

##### javascript

변수 선언과 이벤트리스너
```javascript
//변수 선언과 이벤트리스너
var list = document.querySelector(".list");
var listContent = document.querySelector(".list__content");
var listContent_html = listContent.innerHTML;
var listContent_item_origin = document.querySelectorAll(".list__content-title");
var listContent_originHeight = listContent.scrollHeight;
var count = 0; //함수 반복 카운트

list.addEventListener("scroll", infinite_scroll5);
```

``count`` 변수 이름은 ``js``가 추가되면 변경소지가 있음.

<br>

```javascript
//폭발적인 html 생성으로 사이트가 미친듯이 무거워짐.
function infinite_scroll() {
    if (list.scrollTop > 380) {
        listContent.innerHTML += listContent_html;
    }
}
```

스크롤이 일정한 위치를 지나면 추가적인 ``html`` 이 생성되도록 하였으나,

사이트가 엄~청 무거워져서 결국 멈춰버리는 현상이 발생했다.

<br>

```javascript
//스크롤의 높이가 하단으로 내려갔을 때만 html 을 생성하는 방식으로 제작했더니
//개선이 되었으나, 스크롤을 지속적으로 했을때 무거워지는 이슈 발생.
function infinite_scroll2() {
    if (count === 0 + count && list.scrollTop > 380 + listContent_originHeight * count) {
        listContent.innerHTML += listContent.innerHTML;
        count++;
    }
}
```

화면의 하단에 도달했을 때 생성하는 방식은 결국 해답이 아니었고, 횟수를 제한하거나 방법을 모색해야 했다.


<br>

```javascript
//여러번 반복되어도, 초기화하여서 스크롤링이 유지될 수 있도록 하였으나,
//의도하는 무한 스크롤과는 거리가 있기에 최상단에 추가되었던 li를 제거하는 방법을 모색. 
function infinite_scroll3() {
    if (listContent.scrollHeight >= listContent_originHeight * 2) {
        listContent.innerHTML = listContent_html;
        list.scrollTo(0, 0);
        count = 0;
    }
    if (list.scrollTop >= 24 + (listContent_item_origin.length - 6) * 92 + listContent_originHeight * count) {
        listContent.innerHTML += listContent_html;
        count++;
    }
}
```

사실 가장 의도와 가깝다고 생각해서 구현에 성공한 줄 알았다.

스크롤이 초기화 되면서 자연스럽게 이어지는 것이 아니라, 처음부터 강제로 시작하는 느낌을 들게 했다. 

<br>

```javascript
//li를 제거하는 방법을 사용하여도 최상단에 있던 li가 삭제되면서 스크롤이 튀는 문제 발생
//스크롤의 위치를 보정해주는 방법으로 다시 3번을 수정
function infinite_scroll4() {
    if (listContent.scrollHeight >= listContent_originHeight * 2) {
        var listContent_item = document.querySelectorAll(".list__content-title");

        for (var j = 0; j < listContent_item.length - listContent_item_origin.length; j++) {
            listContent_item[j].remove();
        }
        count = 0;
        //        console.log("stop");
    }
    if (list.scrollTop >= 24 + (listContent_item_origin.length - 6) * 92 + listContent_originHeight * count) {
        listContent.innerHTML += listContent_html;
        count++;
        //        console.log("listcontent:" + listContent.scrollHeight);
        //        console.log("list:" + list.scrollHeight);
        //        console.log("scrollTop:" + list.scrollTop + "\n");
        //        console.log("i:" + i);
        //        console.log("listContent_item.length:" + listContent_item.length);
    }
}
```

사실 3번에서 조금만 바꾸면 되는 문제였는데, 4번은 머릿속으로 생각했던 방법이라서 구현을 해보았다.

하지만 li가 재배열 되면서 3번과 동일하게 화면이 초기화되는 문제가 발생해서 빠르게 손절.

console.log 는 유지보수가 가능한 상대값을 찾기 위해서 한참을 고군분투했다.

<br>

```jacascript
//window.scrollTo(x-coord, y-coord)
//0,0 좌표가 아니라 추가 생성된 아이템의 시작으로 가면 마치 계속 스크롤링 하는 느낌을 줄 수 있다.
function infinite_scroll5() {
    if (listContent.scrollHeight >= listContent_originHeight * 2) {
        listContent.innerHTML = listContent_html;
        list.scrollTo(0, 24 + (listContent_item_origin.length - 6) * 92);
        count = 0;
    }
    if (list.scrollTop >= 24 + (listContent_item_origin.length - 6) * 92 + listContent_originHeight * count) {
        listContent.innerHTML += listContent_html;
        count++;
    }
}
```

한참을 돌고 돌아 다시 찾은 해결방법
 
사실 3번에서 해결할 수 있는 문제였는데 method 속성을 똑바로 확인하지 못한 내 잘못..

스크롤이 컨텐츠 하단으로 이동하면 생성된 아이템의 시작으로 이동하여서 계속 스크롤이 되는 느낌으로 수정했다.

<br>

##### 정리
4시간 남짓을 혼자 끙끙거리면서 ``javascript`` 와 씨름을 했다.

method 를 사용할 때에는 속성이 어떻게 구성되어 있는지 꼭 2번 확인할 것.

내가 구현한 방법이 정답이라고 할 순 없지만 Vanila Javascript 만 사용해서 스스로 구현했다는 것에 뿌듯함을 느낀다.
