## ❓ ivcss是什么
ivcss是封装了css预编译器sass的一种小型函数库。

目前提供的主要核心功能是可以通过缩写emmet自动补全代码。让书写更简单~

## 🛠 开始使用
首先，确保你已经安装好了node环境。
以及会使用sass即其他预编译器。

- 安装ivcss

```shell
npm i ivsss
```

- 引入ivcss
	- 注意引用路径要正确

```scss
@import 'ivcss';
```

- 你也可以用exmple里的文件试行了解
- 下载项目后，使用以下命令

```scss
npm run start
```


## 🎨 写法指南
#### 通过 @include ivcss(); 进行调用
- 传值时，可写参数也可不写参数

```scss
// 如果我们要定义宽度20像素时，我们可以这样写
// 默认是px，所以如果不写入单位，也会自动给你添加
@include ivcss(w20px, w20);
```

**运行结果：** 

```css
width: 20px;
width: 20px;
```

- 百分比输入可以用小p代替也可加百分号
	- 注意：百分号需要加双引号

```scss	
// 若是需要输入百分比的形式
// 因为sass@include传值有规范
// 所以含百分号需要添加引号
// 这里推荐你直接加p，会自动处理成百分比的形式
@include ivcss(w20p, 'w20%');	
```

**运行结果：** 

```css
width: 20%;
width: 20%;
```


- 传颜色时，可不加双引号
	- bg后加rgb形式的需要加 '-'以示区分，因为和background-repeat缩写冲突了。

```scss
// 传颜色
@include ivcss(c#fff, bgc#000, bg-rgba(0,0,0,0.1));
```

**运行结果：**  	
	
```css
color: #fff;
background-color: #000;
background: rgba(0, 0, 0, 0.1);
```

- 传含有空号的值时，使用``进行分隔

```scss	
// 传背景图片
@include ivcss('bg`url("test.png") no-repeat top center`')
```

**运行结果：**  	
	
```css
background: url("test.png") no-repeat top center;
```

- 传某些某些多值参数，如padding、margin，只需用分隔号隔开即可
	- 可不加单位，没有单位的会自动添加单位
	- a可以缩写成auto

```scss
// 传边距ivcss还支持多种方式传值哦~
@include ivcss(p20, p20-30-40 , ma-20-10p-30rem);
```

**运行结果：**

```css
padding: 20px;
padding: 20px 30px 40px;
margin: auto 20px 10% 30rem;
```

- emmet快捷键表中大部分参数皆可支持
 - 【[emmet快捷键文档](https://docs.emmet.io/cheat-sheet/)】

```scss
@include ivcss(pos, poa, db, ovh, txov);	
```

**运行结果：**

```css
position: static;
position: absolute;
display: block;
overflow: hidden;
text-overflow: ellipsis;
```

- ivcss还提供一些其它特殊的值

```scss
// xy + t/b/r/l 会返回四个范围的auto值
@include ivcss(xyt, xyb);
```

**运行结果：**

```css
top: auto;
bottom: auto;
```

- 支持标签写入

```scss
.wrap {
	@include ivcss('[.box]', m0a, ha);
}

@include ivcss('[div .test]', ha);
```
 
 **运行结果：**

```css
.wrap .box {
  margin: 0 auto;
  height: auto;
}

div .test {
  height: auto;
}

```

## ⛏缺点
因为是使用了node-sass进行编写，由于编译器的局限性，
所以造成了某些函数名称以及一些变量外泄，污染了全局空间。
这里，函数名我都使用了ivcss开头进行命名，避免和用户定义冲突。

对于想要学习的人来说，我的代码逻辑会有点混乱，注释不太全，目前还在努力优化代码中。。。

由于是刚上线，因为没有充分的测试，所以可能会有一些未知错误未被发现，不过风险较低。

## ✨ 未来
### 近期
1. 考虑出压缩版
2. 会支持用户自定义，提供三种定义方式
3. 会支持

### 长远
- dart-sass
node-sass如果要写复杂方面的样式逻辑代码，感觉局限性还是挺大的，可能改用dart-sass再重新出一份，dart-sass有很多符合趋势的新功能、接口。

- 下一步发展
	- 提供动画或媒体查询更方便的接口
	- 内置UI组件库
	- 内置动画库

- 其他预编译器：less stylus
今年有时间的话会考虑出。

## 💬 关于
### 版本问题
#### v0.0.1
- 第一个数，代表会做大变动，如重构代码、废除功能等
- 第二个数，单双代表稳定性，单数为不稳定，会出现新功能
- 第三个数，局部优化，或含未发布的小功能测试
- 0版本皆为测试版，1版本会正式上线

### 其它
如果你觉得ivcss不错的话，欢迎到github或gitee上⭐我的项目~
如果有问题的话，请issue板块提出。

### 想说的话
这是我的第一个开源小项目，可能写的不算好。
但是无论是否流行，于众于己，只要本人认为有价值就会一直努力维护下去。

