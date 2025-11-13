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
`<div class="flex allimg">
            <img src="./image/法喜寺5.jpg" alt="">

            <img src="./image/法喜寺1.jpg" alt="">
            <img src="./image/法喜寺2.jpg" alt="">
            <img src="./image/法喜寺3.jpg" alt="">
            <img src="./image/法喜寺4.jpg" alt="">
            <img src="./image/法喜寺5.jpg" alt="">

            <img src="./image/法喜寺1.jpg" alt="">

        </div>`
