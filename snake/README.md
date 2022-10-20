# 001: 贪吃蛇


## 思路

只玩过一种贪吃蛇就是吃吃吃，但是从来也没赢过。。。也不知道后面会怎么样。

我的逻辑一般都是，先搭框架再美化，那我们就先做再说。


元素大概会有以下几个

* 蛇🐍
* 食物
* 边界 
* 格子


那么我们来一个一个创建



## 蛇

先创建个方块充当蛇 30*30 的大小，也方便计算后续增长。
```css
.space {
    position: absolute;
    left: 0;
    top: 0;
    right: 0;
    bottom: 0;
    border: 10px solid green;
}
.snake {
    width: 30px;
    height: 30px;
    background: #000;
}
```
```js
<div class="space">
    <div class="snake"></div>
</div>
```


### 蛇的随机定位

一般来说，贪吃蛇都是初始位置随机分布的，那么根据宽高 + 每个格子大小来决定。

将整个画面都作为蛇行走的空间，根据初始设定，蛇的大小是 30*30 的个头，那么每个格子和蛇是一样大的


```js
var step = 30; //格子 == 步长
var snake = document.querySelector(".snake");
var prev_pos = { x: 0, y: 0 }; // 上一次的位置
var space = document.querySelector('.space');
var width = space.clientWidth, height = space.clientHeight;

// 生成随机坐标
function random_snake_pos(){
    prev_pos.x = random_grid(width) * step;
    prev_pos.y = random_grid(height) * step;
    snake.style.transform = `translate(${prev_pos.x}px, ${prev_pos.y}px)`;
}
// 计算宽度能有多少个格子，再随机选中一个格子，并去小数，保证其不能超出画面。
function random_grid(sum){
    return Math.floor(Math.floor(sum / step) * Math.random())
}
random_snake_pos();
```


接下来，这个蛇要动起来

### 蛇自动游走



```

// 蛇随机游走
function snake_randow_walk() {
    // ...
}
```



### 用户控制蛇的方向

监听键盘事件 [keydown](https://developer.mozilla.org/zh-CN/docs/Web/API/Element/keydown_event)

wasd属于游戏玩家的自我修养hhh😂

按键名称 | e.key | e.keyCode
---------|----------|---------
上  |ArrowUp	|38
左	|ArrowLeft	|37
下	|ArrowDown	|40
右	|ArrowRight	|39
W	|w	        |87
A	|a	        |65
S	|s	        |83
D	|d	        |68

```js
// 监听用户键盘
window.addEventListener('keydown', (e) => {
    console.log(e);

    switch (e.key) {
        case "w": // 上
        case "ArrowUp":
            snake_move({ x: 0, y: -1 }) // 处理方向
            break;
        case "a": // 左
        case "ArrowLeft":
            snake_move({ x: -1, y: 0 })
            break;
        case "s": // 下
        case "ArrowDown":
            snake_move({ x: 0, y: 1 })
            break;
        case "d": // 右
        case "ArrowRight":
            snake_move({ x: 1, y: 0 })
            break;
    }
})
```


