## css 두줄로 swipe animation 생성하기

<br/>

```` css
/* 
    [mdn] scroll-snap-type
    https://developer.mozilla.org/en-US/docs/Web/CSS/scroll-snap-type
*/

.scroll-container {
    scroll-snap-type: y mandatory;
}
````

```` css
/* 
    [mdn] scroll-snap-align
    https://developer.mozilla.org/en-US/docs/Web/CSS/scroll-snap-align
*/

.item {
    scroll-snap-align: center;
}
````