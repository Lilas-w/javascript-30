## 需求拆解
### 1.点击键盘播放声音
- 监听键盘点击事件，触发则执行playSound函数

### 2.定义音频播放函数playSound
- 用html`<audio>`标签属性值规定每个按键对应的声音
- 动态获取按键的keycode
- 立即播放对应声音或停止代码运行（该按键未绑定音乐）
- 使用classList属性新增点击键盘时显示的样式playing类

### 3.制作点击动画
- playing类中已实现放大、加黄色边框和黄色阴影的样式
- 事件绑定：获取字母盒子（样式为key的div）列表，转换为数组。对每个div监听css transition结束事件也即transitionend事件，若触发则执行动画移除函数
- 停止代码运行或移除playing类
- 每个div字母盒子的key类中，已存在transition属性定义过渡效果，结合playing类的样式形成动画。

## 重点难点
### 1.动态获取按键值
css选择器＋模板字面量：
 `audio[data-key = "${e.keyCode}"]`
### 2.音频连发效果
每次点击，`<audio>`音频都从头播放，而非接着上次播放位置继续播放：
```audio.currentTime = 0;```
### 3.将nodeList转换为数组
querySelectorAll返回的是nodeList，类数组。使用Array.from将其转换为数组。

## 知识学习
### 1.`Element.classList`
classList 属性返回元素的类名，作为 DOMTokenList 对象。
该属性用于在元素中添加，移除及切换 CSS 类。
classList 属性是只读的，但可以使用 add() 和 remove() 方法修改它。[Element.classList-MDN](https://developer.mozilla.org/zh-CN/docs/Web/API/Element/classList)

### 2.`transitionend`
transitionend 事件会在 CSS transition 结束后触发. 当transition完成前移除transition时，比如移除css的transition-property 属性，事件将不会被触发.如在transition完成前设置  display 为"none"，事件同样不会被触发。
[transitionend-MDN](https://developer.mozilla.org/zh-CN/docs/Web/API/HTMLElement/transitionend_event)

### 3.`transform`
CSS transform属性允许你旋转，缩放，倾斜或平移给定元素。这是通过修改CSS视觉格式化模型的坐标空间来实现的。[transform-MDN](https://developer.mozilla.org/zh-CN/docs/Web/CSS/transform)

### 4.`box-shadow`
CSS box-shadow属性可设置的值包括阴影的X轴偏移量、Y轴偏移量、模糊半径、扩散半径和颜色。[box-shadow-MDN](https://developer.mozilla.org/zh-CN/docs/Web/CSS/box-shadow)

### 5.`transition`
transition CSS 属性是 transition-property，transition-duration，transition-timing-function 和 transition-delay 的一个简写属性。过渡可以为一个元素在不同状态之间切换的时候定义不同的过渡效果。比如在不同的伪元素之间切换，像是 :hover，:active 或者通过 JavaScript 实现的状态变化。[transition-MDN](https://developer.mozilla.org/zh-CN/docs/Web/CSS/transition)