## ❓ ivcss是什么 what's the ivcss?
ivcss是封装了css预编译器sass的一种小型函数库。<br>
The ivcss is a small function library that encapsulates the precompiler sass of css.

可以让你的sass书写更简单、更便捷。<br>
It makes things like writing scss easier and praticularly faster.

ivcss只有一个接口，非常容易上手，它兼容至少百分之80的emmet的css写法。<br>
ivcss is easy to pick up as it only have one interface, and it compatible with emmet's syntax for css at least 80%.


下面，我们来看一个演示：<br>
Let's look at a small case.
这是一段scss代码，可以看到一共占用了37行。<br>
This is a piece of scss code,and u can see that it takes 37 rows.

```scss
.box{
  width: 300px;
  height: 500px;
  display: inline-block;
  background: #fff;
  border: 1px solid rgba(0,0,0,0.1);
  margin: 10px 20px;
  position: relative;
  .book-image{
    display: block;
    width: 80%;
    height: auto;
    margin: 10% auto 5%;
  }
  .book-name{
    text-align: center;
    overflow: hidden;
    white-space: nowrap;
    text-overflow: ellipsis;
    padding: 10px;
  }
}
.process-bar{
  width: auto;
  height: 10px;
  margin: 0 50px 0 10px;
  background: #ccc;
  position: relative;
  border-radius: 5px;
  .process-active{
    display: block;
    width: 100%;
    height: 100%;
    border-radius: 5px;
    background: rgb(254, 189, 89);
  }
}
```

使用ivcss函数库只需要16行。<br>
Only 16 lines are required by using ivcss.

```scss
import 'ivcss';
.box {
    @include ivcss(w300, h500, dib, bg#fff, "bd1px solid rgba(0,0,0,0.1)", m10-20, por);
  .book-image{
    @include ivcss(db, w80p, ha, m10p-a-5p);
  }
  .book-name {
    @include ivcss(tac, ovh, whsnw, tov, p10);
  }
}
.process-bar{
    @include ivcss(wa, h10, m0-50-0-10, bg#ccc, bdrs5);
  .process-active{
    @include ivcss(db, w100p, h100p, bdrs5, bg-rgb(254,189,89));
  }
}
```

并且还可以再精简到5行。<br>
And it can be leads to fewer lines.

```scss
import 'ivcss';
@include ivcss('[.box]', w300, h500, dib, bg#fff, "bd1px solid rgba(0,0,0,0.1)", m10-20, por);
@include ivcss('[.box .book-image]', db, w80p, ha, m10p-a-5p);
@include ivcss('[.box .book-name]', tac, ovh, whsnw, tov, p10);
@include ivcss('[.process-bar]', wa, h10, m0-50-0-10, bg#ccc, bdrs5);
@include ivcss('[.process-active]', db, w100p, h100p, bdrs5, bg-rgb(254,189,89));
```

## 🛠 开始使用 Get started
首先，确保你已经安装好了node环境。
以及会使用sass即其他预编译器。

- 【Install】安装ivcss

```shell
npm i ivsss
```

- 【Include】引入ivcss
	- 注意引用路径要正确

```scss
@import 'ivcss';
```

- 你也可以用test目录里的文件试行了解<br>
Or, you can use the test folder in the project to experience the ivcss in advance.
- 使用以下命令.<br>
Run the following commands.

```scss
npm install
npm run start
```

## 🎨 使用指南 Guidelines
### 通过 @include  ivcss(); 进行调用
You do have to call @include ivcss() before being used.

- 传值时，可写单位也可不写<br>
Put  params you want into the brackets, if the unit is 'px', you needn't add it.

```scss
@include ivcss(w20px, w20);
```

**【The Result】运行结果：** 

```css
width: 20px;
width: 20px;
```

- 含百分号时需要加引号，否则会报错，推荐你使用p代替<br>
With percent sign, you need to add the quotes, otherwise, it's may report errors, I recommend using the 'p' to replace it.

```scss	
@include ivcss(w20p, 'w20%');	
```

**【The Result】运行结果：** 

```css
width: 20%;
width: 20%;
```


- 传颜色时，可不加引号。bg后加rgb形式的需要加 '-'以示区分，因为和background-repeat缩写冲突了。<br>
Pass the hex color parameter, you can without the quote, but use the rgb need it, especially for "background". beacuse it clashed with "background-repeat".

```scss
@include ivcss(c#fff, bgc#000, bg-rgba(0,0,0,0.1));
```

**【The Result】运行结果：**  	
	
```css
color: #fff;
background-color: #000;
background: rgba(0, 0, 0, 0.1);
```

- 传含有空号的值时，使用``进行分隔，大部分情况下，不加也可以。<br>
Include spaces, the value should be delimited by one pairs of backquote ( ` ).
In most of the case, it's ok if you don't like to add it.

```scss	
@include ivcss('bg`url("test.png") no-repeat top center`');
@include ivcss('bgurl("test.png") no-repeat top center');
```

**【The Result】运行结果：**  	
	
```css
background: url("test.png") no-repeat top center;
background: url("test.png") no-repeat top center;
```

- 传某些某些多值参数，如padding、margin，只需用分隔号隔开即可
	- 可不加单位，没有单位的会自动添加单位
	- a可以缩写成auto

Some multiple values such as "padding" and "margin", using  '-' as a value separator, and also the "auto" can be abbreviated to "a".


```scss
@include ivcss(p20, p20-30-40 , ma-20-10p-30rem);
```

**【The Result】运行结果：**

```css
padding: 20px;
padding: 20px 30px 40px;
margin: auto 20px 10% 30rem;
```

- emmet快捷键表中大部分参数皆可支持
 - 【[emmet快捷键文档](https://docs.emmet.io/cheat-sheet/)】

The ivcss almost support for the abbreviation of css that part of emmet.

```scss
@include ivcss(pos, poa, db, ovh, txov);	
```

**【The Result】运行结果：**

```css
position: static;
position: absolute;
display: block;
overflow: hidden;
text-overflow: ellipsis;
```

- ivcss还提供一些其它特殊的值<br>
Also, ivcss has provided other specific values, like 'xy' plus 't' or 'b' or 'l' or 'r', you can get the "auto".

```scss
// xy + t/b/r/l 会返回四个范围的auto值
@include ivcss(xyt, xyb);
```

**【The Result】运行结果：**

```css
top: auto;
bottom: auto;
```

- 支持选择器写入
Put the selector into the brackets is supported. Please note that it should be first place.

```scss
.wrap {
	@include ivcss('[.box]', m0a, ha);
}

@include ivcss('[div .test]', ha);
```
 
 **【The Result】运行结果：**

```css
.wrap .box {
  margin: 0 auto;
  height: auto;
}

div .test {
  height: auto;
}

```

### 将占位符选择器配置进去 Placeholder selector
同时，你也可以把你的继承类写进去。以下将告诉你如何配置。<br>
Meanwhile, you can also put some placeholder selector in. Now let's see how to configure.

【1】在ivcss_config.scss文件 
```scss
$map-extend-class-user: (
  // 调用名：占位符选择器名
  // call name : placeholder selector name
  ivcss-test-center: 'ivcss-absolute-center',
  ...: ....
);
```

【2】你先在任何你能调用到的地方写下你的占位符选择器。<br>
Putting down this selector , you can get it anywhere.

```scss
%ivcss-absolute-center{
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  margin: auto;
}
```

【3】使用，将调用名直接放进去。<br>
Start using it, just put it in.

```scss
@include ivcss('[.box]', ivcss-test-center, tac, db, w500);
```

【The result】运行结果：

```css
.box {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  margin: auto;
  text-align: center;
  display: block;
  width: 500px;
}
```

### 配置默认单位 configure default units
这个变量$default-units-user将允许自动添加单位，也就是当你没写单位时会自动补全。<br>
This variable "$defult-units-user" will auto-complete when you haven't written the units.

```scss
$default-units-user: rem;
```

使用:
```scss
@include ivcss('[.test-3]', w10, h300px, p20-50px-30);
```

运行结果：
```css
.test-3 {
  width: 10rem;
  height: 300px;
  padding: 20rem 50px 30rem;
}
```

## ✘问题 issue
- 使用@import导入使函数名、变量污染了全局环境。后续考虑用dart-sass重新编写。<br>
The @import rule loads mixins, functions, and variables  while it made they has polluted the global scope.
I'll have a think about that uses dart-sass do it again.
- 测试不够，风险未知。<br>
Testing insufficiently, unknown risk.

(但是用完即走的东西应该不会导致程序崩溃吧。)


## ✨未来 future
- 可能会做一个方便书写动画(animation)和媒体(medio)查询接口
- 关于其他预编译器（Less, styuls），有时间会考虑。


## 🍦其他 Other
第一次开源，有很多不足之处。<br>
The first time open source, there have the insufficient place.
如果你有什么问题，请在github 或gitee的issue版块里指出。<br>
If you have any questions feel free to point out in github or gitee.

Also, please forgive me for broken english.😄


---

ivcss Github: **[ivcss](https://github.com/Sandaydi/ivcss)**<br>
ivscss-tools Github: **[ivscss-tools](https://github.com/Sandaydi/ivscss-tools)**

