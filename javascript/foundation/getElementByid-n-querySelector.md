getElementBy-n-querySelector
=======

### 20210507

``javascript`` 에서 객체를 선택할 때 사용하는 명령어의 차이점에 대한 기록이다.

전혀 생각하고 있지 않다가, 문득 방법이 두개나 있지? 싶어서 찾아본 기록.

이 둘의 차이는 엄연히 다르다는 것을 드디어 알게 되었고,

덕분에 몰랐던 ``node`` 와 ``èlement`` 에 대해 알게 되었다.

<br>

### 개요

#### getElementBy 

```javascript
element = document.getElementById("id");
elements = document.getElementsByClassName("class");
```

``id``, ``class`` 선택자에 일치하는 ``element`` 를 반환한다.

``getElementsByClassName`` 은 ``HTMLcollection`` 을 반환한다.

만약 ``document`` 에 구체적인 ``element`` 가 없다면 ``null`` 을 반환한다.

<br>

#### querySelector

```javascript
element = document.querySelector("#id");
element = document.querySelector(".class");
element = document.querySelectorAll(".class");
```

``id``, ``class`` 선택자에 일치하는 ``document`` 첫번째 ``element`` 를 반환한다.

``querySelectorAll`` 은 ``NodeList`` 를 반환한다.

만약 일치하는 게 없으면 ``null`` 을 반환한다.

<br>


> ClassName, querySelectorAll 복수로 지정됨에 따라 단 하나인 경우에도 배열을 사용해야 한다.

```javascripte
elements.item(0).style.display = "none";
```

<br>


#### HTMLcollection , NodeList

HTMLcollection : name, id, index, number 로 HTMLcollection의 항목에 접근할 수 있다. 

NodeList : index Number 로만 접근할 수 있다.


```
구체적인 요소를 선택할 때, querySelector 를 사용한다.

그러나 getElementBy 가 더 빠르고, 잘 지원된다는 점을 기억할 것.
```

출처 : https://guinatal.github.io/queryselector-vs-getelementbyid/
