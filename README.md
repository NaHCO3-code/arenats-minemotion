# MineMotion
简单的动画库

# Example
```javascript
const box = UiBox.create();
box.size.offset.x = 100;
box.size.offset.y = 100;
box.backgroundColor.r = 255;
box.backgroundColor.g = 0;
box.backgroundColor.b = 0;
box.parent = ui;
;(async function(){
  // 在1s内移动到(300, 200)
  await MineMotion.fromTo(
    box.position.offset, // 要进行变换的对象
    1000,                // 变换时间，单位为ms
    { x: 0, y: 0 },      // 起始值
    { x: 300, y: 200 },  // 目标值
    Ease.easeInOut       // 缓动函数
  ).wait;

  // 变色的同时移动到(0, 0)
  // 这里不await，否则会先变色后移动
  MineMotion.fromTo(
    box.backgroundColor, 
    1000, 
    { r: 255, g: 0, b: 0 }, 
    { r: 0, g: 255, b: 0 }, 
    Ease.easeInOut
  );
  await MineMotion.fromTo(
    box.position.offset,
    1000,
    { x: 300, y: 200 },
    { x: 0, y: 0 },
    Ease.linear         // 使用线性缓动函数
  ).wait;
})();
```
效果：
![](https://static.codemao.cn/pickduck/rkeYhTh-kx.gif?hash=FgTcHWUYxdyQDRPghdjzFeYTKTuc)

# API
## MineMotion.fromTo(obj, duration, start, end, ease)
创建一个动画，从start到end，在duration时间内完成。
### definition
```javascript
static fromTo<T extends Object>(
  obj: T, 
  duration: number, 
  from: Partial<T>,
  to: Partial<T>,
  ease: (rate: number) => number = Ease.linear
)
```
## MineMotion.enable()
启用动画。默认导入时自动启用。

## MineMotion.disable()
禁用动画。

# Classes
## MineMotion
动画类。通过此类控制动画。
### Methods
#### pause()
暂停动画。
#### resume()
继续动画。
### Properties
#### wait: Promise&lt;void&gt;
动画完成时，该Promise会被resolve。

# Constants
## Ease
一些常见缓动函数的集合。

你也可以自己编写缓动函数或使用网上的缓动函数，只要它们是符合形如 $f: [0, 1] \rightarrow [0, 1]$ 的函数即可。
### linear
线性缓动函数。
### easeInOut
平滑缓动函数。
### easeIn
平滑缓入函数。
### easeOut
平滑缓出函数。
### sine
正弦缓动函数。