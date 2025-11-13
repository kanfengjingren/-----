# 无缝轮播图
这是我第一个正经在github上发布的小项目，这个项目可能比较简陋也比较简单，但是我觉得作为我的一个起点完全没问题
## 框架和准备工作
由于之前使用过**tailwind css**所以这里也使用了这一种**css原子化框架** 
配置方法见：[Tailwind CSS配置](https://www.runoob.com/tailwindcss/tailwindcss-config.html)
然后是用vite指令快速启动，这个非常简单，但是为了提醒我自己，我还是写一下
- 下载安装[node.js](https://nodejs.cn/download/)
- 在根目录执行命令 `npm i vite -D`
- 向**package.json**的大括号中添加这段代码
  `"scripts": {
    "dev": "vite"
  },`
- 最后执行命令`npm run dev`

## 基本的html结构
`

      <div class="flex allimg">
  
            <img src="./image/法喜寺5.jpg" alt="">

            <img src="./image/法喜寺1.jpg" alt="">
            <img src="./image/法喜寺2.jpg" alt="">
            <img src="./image/法喜寺3.jpg" alt="">
            <img src="./image/法喜寺4.jpg" alt="">
            <img src="./image/法喜寺5.jpg" alt="">

            <img src="./image/法喜寺1.jpg" alt="">

        </div>`

## 实现思路
原理其实不难，就是在头和为各放一张头和尾的复制品，在需要头尾切换的时候，就先转到复制品，然后瞬间定位回原来的头和尾的位置，然后继续向后轮播。在这个图片的大容器的父级容器中设置`overflow: hiddend`就可以让暴露出来的图片隐藏

### 代码实现
直接来看**nextImg()**这个函数的实现

```

function nextImg() {
            //让div整体向左移
            i++;
            if (i < 6) {
                console.log(i);
                console.log(-(i * 600));
                span.innerHTML = text[i - 1];
                allimg.style.transform = `translate(${-(i * 600)}px)`;
                //清除样式
                clearClass();
                //让点变白
                li[i - 1].classList.add('dotactive');
            } else {
                allimg.style.transform = `translate(${-(i * 600)}px)`;
                clearClass();
                span.innerHTML = text[0];
                li[0].classList.add('dotactive');
                //等待这个过度结束之后，再进行下面的操作
                //怎么去判断这个有没有结束呢？用这个事件监听
                allimg.addEventListener('transitionend', function () {
                    //这里面的过程需要关闭动画和过渡效果，怎么关闭呢？
                    allimg.style.transition = 'none';
                    i = 1;
                    allimg.style.transform = `translateX(-${600*i}px)`;
                }, { once: true });
            }
            allimg.style.transition = 'all .5s';
        }

```
因为我们想要从实际的第一张开始（即这7张图片中的第二张），所以需要在外面设置最开始展示的位置是 **-600px**。<br>
i从1开始循环，当时间到了触发定时函数时，先让i自增，然后我们通过``` allimg.style.transform = `translate(${-(i * 600)}px)` ```来实现图片的移动<br>
当**i=6**时，也就是当前已经是最后一张，需要向第一张进行轮播了。<br>
为了丝滑的进行，我们特意放上复制的第一张**copy_1**,让最后一张先轮播到这张图片，并且更改小点和显示的图片文字信息<br>
使用事件监听**transitionend**,一旦这个轮播的过渡动画结束，关闭过渡效果`allimg.style.transition = 'none';`<br>
将i重置为1，并且瞬间定位到图片一的位置，视觉欺骗说是<br>
最后整个过程完成后，开启过渡效果
preImg()函数的实现也是一样

## 节流
因为我发现点击下一张或者上一张的按钮，短时间内点击次数太多，所以加上了节流操作
😋👍
# 希望能帮助到你
