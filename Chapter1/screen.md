## 获取手机屏幕宽度、高度



### 网页可见区

```javascript
// document.documentElement --> html/root
// document.body --> body

// 可见区宽
document.body.clientWidth
document.documentElement.clientWidth
document.body.offsetWidth // 包括边线的宽
document.documentElement.offsetWidth

// 可见区高
document.body.clientHeight
document.documentElement.clientWidth
document.body.offsetHeight // 包括边线的宽
document.documentElement.offsetHeight

```



### 网页全文

```javascript
// 全文宽
document.body.scrollWidth

// 全文高
document.body.scrollHeight
```



### 网页滚动

```javascript
// 滚动条顶部距离
document.body.scrollTop

// 滚动条左侧距离
document.body.scrollLeft
```



### 屏幕分辨率

```javascript
// 屏幕高
window.screen.height

// 屏幕宽
window.screen.width

// 屏幕可用工作区，减去诸如窗口工具条之类的界面特征
// 高度
window.screen.availHeight

// 宽度
window.screen.availWidth
```



## 滚动触底事件

页面滚动触底翻页是移动端比较常见的需求

### 监听滚动

使用 `element.addEventListener` 添加事件队列

直接使用 `element.onscroll` 会存在冲突问题，这里的冲突问题是指当这个节点定义了多个滚动事件时，只会生效最后一个

```javascript
// element 一般为window
element.addEventListener('scroll', function() {
    // do sth.
})
```



### 判断触底

当可视区高度 + 滚动条顶部距离 >= 全文高度

``` javascript
if (element.offsetHeight + element.scrollTop >= element.scrollHeight) {
    // do sth.
}
```

这样判断还是不够，当需要监听容器为 `window` 时，就需要另外计算容器的高度

```javascript
var element = document.documentElement || document.body;
if (element.clientHeight + element.scrollTop >= element.scrollHeigh) {
    // do sth.
}
```



### 整理

```javascript
/**
 * 监听滚动触底事件
 * @options[element]，监听滚动的元素，默认指向window
 * @options[callback]，触底回调
 * @options[threshold]，到达底部多少距离触发回调
 */
function evBottomOut(options) {
    if (typeof options == 'function') {
        options = {callback: options};
    }
    if (typeof options.callback !== 'function') return;
    
    var element = options.element;
    var isWinow = !element || element.nodeType != 1;
    
    var elListener = isWinow ? window : element;
    
    var threshold = isNaN(threshold) ? 0 : threshold;
    
    element = isWinow ? (document.documentElement || document.body) : element;
    
    elListener.addEventListener('scroll', function() {
        var clientH = isWinow ? element.clientHeight : element.offsetHeight;
        var scrollT = element.scrollTop;
        var scrollH = element.scrollHeight;
        
        if (clientH + scrollT - threshold >= scrollH) {
            options.callback();
        }
    })
}
```



