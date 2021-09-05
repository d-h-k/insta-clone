## 이벤트 델리게이션이란?
- 부모에게 이벤트를 떠넘기는(위임)하는 방식
- 컨텐츠박스를 클릭했을때, 특정 클릭이벤트에 대해서 부모에게 이벤트 처리를 넘기는 방식
```js
function delegatFunc(e) {
    let elem = e.target;
    console.log(elem);

    while(!elem.getAttribute('data-name')) {
        elem = elem.parentNode; // 부모노드 찾기
        if(elem.nodeName == 'BODY') {
            return; // 바디까지 올라갔는데도(끝까지) 못찾으면 >> 빈값으로 만들고 끝내라
        }
    }

    if(elem.matches('[data-name-"heartbeat"]')) {
        console.log('하트비트');
    }

    if(elem.matches('[data-name-"bookmark"]')) {
        console.log('bookmark');
    }


    if(elem.matches('[data-name-"share"]')) {
        console.log('share');
    }


    if(elem.matches('[data-name-"more"]')) {
        console.log('more');
    }
    
    elem.classlist.toggle('on');
}
```


## 리사이즈 펑션

```js
function resizeFunc() {

    console.log('resize!!');

    if (pageYOffset >= 10) {
        let calcWidth = (window.innerWidth * 0.5) + 167;
        sidebox.style.left = calcWidth + 'px';
    }


    if (matchMedia('screen and (max-width : 800px)').matches) {
        for (let i = 0; i < variableWidth.length; i++) {
            variableWidth[i].style.width = window.innerWidth - 20 + 'px';
        }
    } else {
        for (let i = 0; i < variableWidth.length; i++) {
            if (window.innerWidth > 600) {
                variableWidth[i].removeAttribute('style');
            }
        }
    }

}
```

## 스크롤 펑션

```js

function scrollFunc() {
    var scrollHeight = pageYOffset + window.innerHeight;
    var documentHeight = document.body.scrollHeight;

    console.log(pageYOffset);
    if (pageYOffset >= 10) {
        header.classList.add('on');
        if (sidebox) {
            sidebox.classList.add('on');
        }

        resizeFunc();


    } else {
        header.classList.remove('on');

        if (sidebox) {
            sidebox.classList.remove('on');
            sidebox.removeAttribute('style');
        }

    }

    console.log('scrollHeight : '+scrollHeight);
    console.log('documentHeight : ' +documentHeight);

    if (scrollHeight >= documentHeight) {

        var page = document.querySelector('#page').value;

        // page = parseInt(page) + 1;
        // page = parseInt(page) + 1;
        document.querySelector('#page').value = parseInt(page) + 1;
        // $('#page').val(parseInt(page) + 1);

        callMorePostAjax(page);

        if(page > 10){
            return;
        }

    }

}
```