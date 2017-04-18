学习Pixi
=============

一步一步的介绍如何用[Pixi渲染引擎](https://github.com/pixijs/pixi.js) 制作游戏和交互性多媒体。 **[更新至 Pixi v4.0.0](https://github.com/pixijs/pixi.js/releases/tag/v4.0.0)**. 如果你喜欢本教程 [你肯定会喜欢这本书，它包含了更多80%的内容！](http://www.springer.com/us/book/9781484210956)

### 目录表：
1. [介绍](#introduction)
2. [建立环境](#settingup)
  1. [安装Pixi的简单方法](#installingpixithesimpleway)
  2. [通过Git安装Pixi](#installingpixiwithgit)
  3. [通过Node和Gulp安装Pixi](#installingpixiwithnodeandgulp)
3. [创建舞台的渲染器](#renderer)
4. [Pixi 精灵](#sprites)
5. [把图片加载到纹理缓存里](#loading)
6. [展示精灵](#displaying)
  1. [通过别名](#usingaliases)
  2. [更过关于加载的小技巧](#alittlemoreaboutloadingthings)
    1. [从普通JavaScript图像对象或画布中创建一个精灵](#makeaspritefromanordinaryjavascriptimageobject)
    2. [为已加载的文件指定一个名字](#assigninganametoaloadingfile)
    3. [监控加载进度](#monitoringloadprogress)
    4. [更多关于Pixi加载器](#moreaboutpixisloader)
7. [定位精灵](#positioning)
8. [尺寸和缩放](#sizenscale)
9. [旋转](#rotation)
10. [从背景子图像集中制作精灵](#tileset)
11. [使用纹理地图集（texture atlas）？](#textureatlas)
12. [加载纹理地图集](#loadingatlas)
13. [从一个已加载的纹理地图集中制作精灵](#createsprites)
14. [移动精灵](#movingsprites)
15. [使用速度属性](#velocity)
16. [游戏状态](#gamestates)
17. [键盘动作](#keyboard)
18. [分组的精灵](#grouping)
  1. [局部和全局位置](#localnglobal)
  2. [给分组精灵用 ParticleContainer](#spritebatch)
19. [Pixi的图元](#graphic)
  1. [矩形](#rectangle)
  2. [圆形](#circles)
  3. [椭圆](#ellipses)
  4. [圆角矩形](#roundedrects)
  5. [线条](#lines)
  6. [多边形](#polygons)
20. [展示文字](#text)
21. [碰撞检测](#collision)
  1. [ hitTestRectangle 函数](hittest)
22. [实战学习: 宝藏猎手](#casestudy)
  1. [利用 setup 函数初始化游戏](#initialize)
    1. [创建游戏场景](#gamescene)
    2. [制作地牢, 门, 探险者 和 宝藏](#makingdungon)
    3. [制作一堆怪物](#makingblob)
    4. [制作血条](#healthbar)
    5. [制作消息文字](#message)
  2. [玩游戏](#playing)
  3. [移动探险者](#movingexplorer)
    1. [控制移动](#containingmovement)
  4. [移动怪物](#movingmonsters)
  5. [碰撞检查](#checkingcollisions)
  6. [到达出口并结束游戏](#reachingexit)
23. [更多关于精灵](#spriteproperties)
24. [更进一步](#takingitfurther)</br>
  i.[Hexi](#hexi)</br>
25. [支持该项目](#supportingthisproject)

<a id='introduction'></a>
介绍
------------

PixiJs是一个速度极快的2D精灵图渲染引擎。这意味着什么？意味着它能帮你展示，驱动和管理富有交互性的图形以便于制作游戏和通过使用JavaScript以及其他HTML5技术而创建的一系列应用。它有一套合理的、整齐的API并且提供了许多有用的特性，像支持纹理地图集并且还提供了动画精灵图（交互式图像）的简化流程。它也给你了一个完整的场景图以便于你能够创建嵌套的精灵图（一个精灵图在另一个精灵图里面），与此同时让你可以直接在精灵图上绑定鼠标和触摸事件。最重要的是，Pixi让你能够按照自己所想和所需，适应自己的编码风格，和其他有用的框架完美的结合。

Pixi的API是由Macromedia / Adob​​e Flash开创一个经过磨练和测试的API的改良版。原Flash开发者使用起来会得心应手。目前其他的一些精灵渲染框架用了相似的API：CreateJS、Starling、Sparrow和苹果的SpriteKit。Pixi的API的优点在于它致力于通用性：它不是一个游戏引擎。这一点很好，因为它给你了一个完全的自由让你做你任何想做的东西，把你自己的游戏引擎和它揉和在一起。

在本教程中，你将弄清楚如何结合Pixi的强大的图像渲染引擎以及场景图去制作游戏。你也会学习如何通过一个纹理背景图去准备你的游戏图像，如何通过质子粒子引擎去制作粒子效果，以及如何把Pixi整合到自己的游戏引擎中。但是Pixi并不只是为游戏而生的 - 你可以用这些相同的技术去创造任何可交互的多媒体应用。这意味着手机应用！

在开始学习本教程之前你需要了解什么？

你应该对HTML以及JavaScript有一个适当的理解。你不需要成为一个专家，只需要做一个渴望学习的富有雄心的初学者。如果你不了解HTML和JavaScript，最好的开始学习的地方是这本书：

[Foundation Game Design with HTML5 and JavaScript](http://www.apress.com/9781430247166)

我能确信的一点的是它是一本最好的书，因为是我写的！（手动斜眼笑- -）

这里也有一些非常好的互联网资源能帮助你学习：

[Khan Academy: Computer
Programming](http://www.khanacademy.org/computing/cs)

[Code Academy:
JavaScript](http://www.codecademy.com/tracks/javascript)

选择最适合你学习方式的就行了。

好了，明白了吗？
你了解了什么是JavaScript变量、函数、数组以及对象以及如何使用它们吗？你明白了什么是[JSON数据格式文件](http://www.copterlabs.com/blog/json-what-it-is-how-it-works-how-to-use-it/)了吗？你是否使用过[Canvas绘图 API](https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API/Drawing_graphics_with_canvas)呢？

为了使用Pixi，你也需要在你项目的根目录下开启一个web服务器。你知道什么是web服务器以及如何在你的项目文件夹里启动吗？最好的方式是使用[node.js](http://nodejs.org)，然后十分简单的安装一个[http-server](https://github.com/nodeapps/http-server)。然而，如果你想那么做，你需要在Unix的命令行中舒适的工作。你可以在[这个视频里](https://www.youtube.com/watch?feature=player_embedded&v=cX9ASUE3YAQ)学习如何使用Unix，当你完成时候，接着学习[这个视频](https://www.youtube.com/watch?v=INk0ATBbclc)。你应当学习如何使用Unix - 它只会耗费你几个小时的时间去学习而且它是一个和电脑交互的非常简单有趣的方式。

但是如果你不想搅入刚才提到的命令行的乱麻中，试试Mongoose服务器：

[Mongoose](http://cesanta.com/mongoose.shtml)

或者，只需要用出色的[Brackets text
editor](http://brackets.io)去编写你的所有代码。当你在Brackets的主要工作区点击那个闪电按钮，它会自动为你启动一个web服务器和浏览器。

现在如果你觉得你准备好了，那就继续往下读吧！

（读者要求：这是一个 *在线文档*。如果你对某个指定的细节有任何问题或者需要任何相关内容的解释，请在这个GitHub仓库中创建一个 **issue**，我会更新更多的信息。）

<a id='settingup'></a>
建立环境
----------

在你开始写代码之前，为你的项目创建一个文件夹，然后在项目的根目录下启动一个web服务器。如果你不开启一个web服务器的话，Pixi将不会工作。

接下来，你需要安装Pixi。这里有两种方式：**简单**的方法，用 **Git** 或者用 **Gulp 和 Node**。 

<a id='installingpixithesimpleway'></a>
### 安装Pixi的简单方法

本介绍用的Pixi版本是 **v4.0.0**，你可以在[Pixi's release page for v4.0.0](https://github.com/pixijs/pixi.js/releases/tag/v4.0.0)找到`pixi.min.js`文件。或者你可以从[Pixi's main release page](https://github.com/pixijs/pixi.js/releases)获取最新的版本。

这个文件就是使用Pixi的全部所需。你可以忽略此仓库中的其他所有文件：**你不需要它们**。

接下来，创建一个基本的HTML页面，然后用`<script>` 标签去链接刚才你下载的`pixi.min.js` 文件，这个`<script>` 标签的 `src`应当是你根目录的相对路径。你的`<script>` 标签应当看起来像这样
```html
<script src="pixi.min.js"></script>
```
这是一个完整的HTML页面，你可以用它来加载Pixi然后测试一下它是可以工作的：
```html
<!doctype html>
<html>
<head>
  <meta charset="utf-8">
  <title>Hello World</title>
</head>
  <script src="pixi.min.js"></script>
<body>
  <script type="text/javascript">
    var type = "WebGL"
    if(!PIXI.utils.isWebGLSupported()){
      type = "canvas"
    }

    PIXI.utils.sayHello(type)
  </script>
</body>
</html>
```

如果Pixi载入成功，
下面的信息将会在你的web浏览器的JavaScript控制台中默认显示出来：
```
 Pixi.js 4.0.0 - ✰ WebGL ✰      http://www.pixijs.com/    ♥♥♥ 
```

现在你可以通过Pixi来工作啦！

<a id='installingpixiwithgit'></a>
### 通过Git安装Pixi

你也可以通过Git安装使用Pixi。（啥是 **git**？如果你不知道，[你可以在这儿弄清楚](https://github.com/kittykatattack/learningGit)。）用Git安装有一些优势就是：你可以只通过在命令行运行 `git pull origin master` 去更新Pixi到最新的版本。并且，如果你觉得你在Pixi中发现了一个bug，你可以修复它并在主仓库中提交一个修复bug的pull请求。

为了通过Git克隆Pixi仓库， `cd`进入你的项目根目录并键入：
```
git clone git@github.com:pixijs/pixi.js.git
```
它会自动创建一个名为`pixi.js`的文件夹而且会加载**最新版本**的Pixi。请时刻记住，本手册是围绕 *version 4.0.0* 展开的。通过简单的切换分支的方式：
```
git checkout tags/v4.0.0
```
可以获取4.0版本。

Pixi安装之后，创建一个基本的HTML文档，然后用`<script>`标签从Pixi的`bin`文件夹里加载`pixi.js`文件：
```html
<script src="pixi.js/bin/pixi.js"></script>
```
(If you prefer, you could link to the `pixi.min.js` file instead as I
suggested in the previous section. The
minified file might actually run slightly faster, and it will
certainly load faster. The advantage to using the
un-minified plain JS file is that if the compiler thinks there's a bug in Pixi's
source code, it will give you an error message that displays the questionable code
in a readable format. This is useful while you're working on a
project, because even if the bug isn't in Pixi, the error might give
you a hint as to what's wrong with your own code.)

In this **Learning Pixi** repository (what you're reading now!) you'll find a folder called
`examples`. Open it and you'll find a file called `helloWorld.html`.
Assuming that the webserver is running in this repository's root directory, this is
how the `helloWorld.html` file correctly links to Pixi and checks that it's
working:
```html
<!doctype html>
<html>
<head>
  <meta charset="utf-8">
  <title>Hello World</title>
</head>
<body>
  <script src="../pixi.js/bin/pixi.js"></script>
</body>
</html>
```
If Pixi is linking correctly, something like this will be displayed in your web browser's JavaScript console by default:
```
 Pixi.js 4.0.0 - ✰ WebGL ✰      http://www.pixijs.com/    ♥♥♥ 
```

<a id='installingpixiwithnodeandgulp'></a>
### Installing Pixi with Node and Gulp

You can also install Pixi using [Node](https://nodejs.org) and [Gulp](http://gulpjs.com). If you need
to do a custom build of Pixi to include or exclude certain features,
this is the route you should take. [See Pixi's GitHub repository for
details on how](https://github.com/GoodBoyDigital/pixi.js). But, in general
there's no need to do this.

<a id='renderer'></a>
创建渲染器和舞台
-------------------------------

现在可以开始使用Pixi了！

但是咋使用呢？

第一步就是创建一个矩形显示区域用来展示图片。可以用Pixi的`renderer`对象可以创建。它能自动生成一个HTML`<canvas>`节点并且能指定如何在Canvas上展示你的图像。然后你需要创建一个特殊的Pixi`Container`对象名为`stage`。正如你将看到，这个舞台对象会被用作持有所有你想让Pixi展示的东西的根容器。

你需要写如下代码去创建一个`renderer` 和 `stage`。把这段代码通过`<script>`便签括起来并添加到你的HTML文档中：

```js
//Create the renderer
var renderer = PIXI.autoDetectRenderer(256, 256);

//Add the canvas to the HTML document
document.body.appendChild(renderer.view);

//Create a container object called the `stage`
var stage = new PIXI.Container();

//Tell the `renderer` to `render` the `stage`
renderer.render(stage);
```

这是你开始使用Pixi的你需要写的最基本的代码。它会生成一个黑色的256*256大小的Canvas节点并且把它添加到你的HTML文档中。当你运行这段代码的时候，会有如下效果：

![基本展示](/examples/images/screenshots/01.png)

恩，一个[黑色的正方形](http://rampantgames.com/blog/?p=7745)！

Pixi的`autoDetectRenderer` 方法能计算出是用Canvas的绘图API还是WebGL去渲染图像，这取决于哪一种可用。它的第一个和第二个参数是canvas的宽和高。不仅如此，你可通过可配置的第三个参数去设置其他一些配置。第三个参数是一个字面量对象，这儿有一个如何通过它去设置抗锯齿、透明和分辨率的例子：
```js
renderer = PIXI.autoDetectRenderer(
  256, 256,
  {antialias: false, transparent: false, resolution: 1}
);
```
第三个参数是可配置的 - 如果你很满意Pixi的默认设置你可以不用管它，通常也并没有需要去改变他们。（但是，如果你需要，请查询有关[Canvas
Renderer](http://pixijs.download/release/docs/PIXI.CanvasRenderer.html)和[WebGLRenderer](http://pixijs.download/release/docs/PIXI.WebGLRenderer.html)
了解更多信息）

这些配置都是干啥的？
```js
{antialias: false, transparent: false, resolution: 1}
```
`antialias`（抗锯齿）能够平滑字体和图元的边缘。（WebGL的图形保真并不适用于所有的平台，所以你需要在你游戏的目标平台上测试一下。）`transparent`能让canvas背景透明。`resolution`能使在不同分辨率和像素密度的显示器上工作起来更简单。设置分辨率有点儿稍微超出本教程的范畴，查看[Mat Grove's
explanation](http://www.goodboydigital.com/pixi-js-v2-fastest-2d-webgl-renderer/)中关于如果使用`resolution`可以找到所有细节。但是通常呢，在大多数项目里只需要保持 `resolution` 的值为1就好了。

（注意：渲染器有一个额外的、第四个选项叫 `preserveDrawingBuffer` 默认为 `false`。唯一需要设置它为 `true`的理由就是你是否需要在一个WebGL canvas上下文中调用Pixi的专用`dataToURL`方法。）

Pixi的渲染器对象会默认为WebGL，因为WebGL不可思议的快，并且能够让你使用一些将来你会学到的壮观的视觉效果。但是如果你需要强制使用Canvas绘图API渲染，你可以这样做：
```js
renderer = new PIXI.CanvasRenderer(256, 256);
```
只有前两个参数是必要的：'width' 和 'height'。

你可以像这样强制WebGL渲染：
```js
renderer = new PIXI.WebGLRenderer(256, 256);
```
`renderer.view` 对象只是一个再普通不过的 `<canvas>` 对象，所以你可以像控制其他任何 canvas 对象一样控制它。这里告诉你如何给canvas一个虚线边框：
```js
renderer.view.style.border = "1px dashed black";
```
如果你想在创建canvas后改变它的背景颜色，设置 `renderer` 对象的 `backgroundColor` 属性为其他任何十六进制的颜色值：
```js
renderer.backgroundColor = 0x061639;
```
如果你想获取 `renderer` 的宽和高，用 `renderer.view.width` 和 `renderer.view.height`。

（重要提示：尽管 `stage` 也有 `width` 和 `height` 属性，*它们不是指渲染窗口的大小*。舞台的 `width` 和 `height` 只是告诉你你放的东西所占用的区域 - 更多解释将会在下面看到！）

可以用 `renderer` 的 `resize` 方法设置任何新的 `width` 和 `height` 值去改变 canvas 的大小。但是，请确保canvas和分辨率是大小相匹配的，设置 `autoResize` 为 `true`。
```js
renderer.autoResize = true;
renderer.resize(512, 512);
```
如果你想让canvas占据整个窗口，你可以设置CSS样式并且调整渲染器的大小为浏览器窗口的大小。
```css
renderer.view.style.position = "absolute";
renderer.view.style.display = "block";
renderer.autoResize = true;
renderer.resize(window.innerWidth, window.innerHeight);
```
但是如果你那么做了，请确保用下面的一小段css代码设置你所有的HTML节点的默认内边距和外边距为0：
```html
<style>* {padding: 0; margin: 0}</style>
```
（在上面代码中的星号：*，是CSS的『通用选择符』，表示『在HTML文档中的所有标签』。）

如果你想让canvas可以自动缩放适应适应所有的浏览器窗口大小，你可以用[这个自动缩放窗口函数](https://github.com/kittykatattack/scaleToWindow)。

<a id='sprites'></a>
Pixi 精灵
------------

在上一个章节，你学会了如果去创建一个 `stage` 对象：
```js
var stage = new PIXI.Container();
```
`stage` 是一个Pixi `Container` 对象。你可以把这个容器想象成一个可以把你所有想放的东西放进去的一种空盒子。
我们创建的 `stage` 对象是在你创建的场景中所有可视物体的根容器。Pixi需要你有一个根容器，因为 `renderer` 需要有一个东西去渲染上去：
```js
renderer.render(stage);
```
不管你往这个 `stage` 里面放什么都会被渲染到canvas上面。现在这个 `stage` 是空的，但是一会儿我们就会往里面放一些东西。

（注意：你可以给你的根容器任何你名字。如果你喜欢的话可以把它叫做 `scene` 或者 `root`。`stage` 这个名字仅仅是一个古老而有用的约定，我们也会在本教程中一直使用它。）

那么你想在舞台上放什么？特殊的图片对象被叫做 **精灵图**。你可以控制它们的位置，尺寸以及其他许多有用的可以制作交互式动画图形的属性。学习如何控制一个精灵图对学习如何使用Pixi来说是十分重要的。如果你知道了如何制作精灵图并把它们添加到舞台上，你才刚刚迈出了制作游戏的一小步、

Pixi有一个 `Sprite` 类，它是创建游戏精灵的通用方式。这里还有三个主要的方式去创建它们：

- 使用单独一个图片文件
- 使用**图片集** 的一个子图像。图片集是一个单独的，大的图像，它包含了所有游戏中你需要的图片。（译者注：就是我们说的雪碧图吧）。
- 使用**纹理图集**（一个定义了在雪碧图中一个图片的位置和大小的JSON文件）

你将会学习所有的三种方式，但是，之前，让我们先弄清楚在你利用pixi展示图片之前你需要了解哪些关于图片的知识。

<a id='loading'></a>
加载图像到纹理缓存中
-------------------------------------

因为Pixi通过WebGL把图像渲染到GPU上面，图像需要被格式化为GPU可以处理的方式。一个为WebGL准备的图像称为**纹理**。在你制作精灵展示图像之前，你需要把一个原始的图像转化为一个WebGL纹理。为了保持所有的东西都能在底层快速高效的工作，Pixi使用了一个 **纹理缓存** 去存储和引用所有精灵图所需要的纹理。纹理的名字是字符串，指向图片文件的位置。这意味着如果你有一个纹理是从`"images/cat.png"`载入的，那么你可以在纹理缓存中通过这种方式来找到它：
```js
PIXI.utils.TextureCache["images/cat.png"];
```
纹理都是已WebGL兼容格式存储的，这能让Pixi渲染器高效率的工作。然后你可以利用 `Sprite` 类通过用纹理来制作一个新的精灵。
```js
var texture = PIXI.utils.TextureCache["images/anySpriteImage.png"];
var sprite = new PIXI.Sprite(texture);
```
但是你如何加载一个图片并把它转化为一个纹理？用Pixi的内置 `loader` 对象。

Pixi强大的`loader` 对象是你加载任何一种图像的全部所需。这里告诉你了如何加载一个图像并在图像加载完成之后调用 `setup` 函数。
```js
PIXI.loader
  .add("images/anyImage.png")
  .load(setup);

function setup() {
  //This code will run when the loader has finished loading the image
}
```
[Pixi开发团队推荐](http://www.html5gamedevs.com/topic/16019-preload-all-textures/?p=90907)
如果你使用了加载器，你应该通过引用纹理中的`loader` 的 `resources` 对象来创建精灵，像这样：
```js
var sprite = new PIXI.Sprite(
  PIXI.loader.resources["images/anyImage.png"].texture
);
```
这里有一个例子，可以通过它来加载一个图像，调用`setup` 函数，并且从加载过的图像中创建一个精灵：
```js
PIXI.loader
  .add("images/anyImage.png")
  .load(setup);

function setup() {
  var sprite = new PIXI.Sprite(
    PIXI.loader.resources["images/anyImage.png"].texture
  );
}
```
我们将在本教程中使用这种一般的格式来图像和创建精灵。

你可以通过一连串的 `add` 方法来一次性加载许多图像：
```js
PIXI.loader
  .add("images/imageOne.png")
  .add("images/imageTwo.png")
  .add("images/imageThree.png")
  .load(setup);
```
更好的做法是，把所有的你想加载文件放到一个数组里，通过一个`add`方法：
```js
PIXI.loader
  .add([
    "images/imageOne.png",
    "images/imageTwo.png",
    "images/imageThree.png"
  ])
  .load(setup);
```
`loader`也可以让你加载JSON文件，下面你将会学习到。

<a id='displaying'></a>
展示精灵
------------------

在你加载了一个图片并用它制作了一个精灵之后，想要在canvas上看到它，还有两件事情你不得不做。

-1. 你需要通过 `stage.addChild` 方法把精灵添加到 Pixi的 `stage`中：
```js
stage.addChild(cat);
```
舞台是容纳所有精灵的主要容器。

-2. 你需要告诉Pixi的 `renderer` 去渲染这个舞台。
```js
renderer.render(stage);
```
**在你不做以上两步之前任何精灵你都看不到**

在我们继续之前，让我们看一个如何用刚才学的东西去展示一个单独的图片的实际例子。在 `examples/images` 文件夹中，你能找到一个64*64的猫的PNG图片。

![基本展示](/examples/images/cat.png)

加载图像，创建一个精灵，并把它展示在Pixi舞台上的所有的JavaScript代码：
```js
var stage = new PIXI.Container(),
    renderer = PIXI.autoDetectRenderer(256, 256);
document.body.appendChild(renderer.view);

//Use Pixi's built-in `loader` object to load an image
PIXI.loader
  .add("images/cat.png")
  .load(setup);

//This `setup` function will run when the image has loaded
function setup() {

  //Create the `cat` sprite from the texture
  var cat = new PIXI.Sprite(
    PIXI.loader.resources["images/cat.png"].texture
  );

  //Add the cat to the stage
  stage.addChild(cat);
  
  //Render the stage   
  renderer.render(stage);
}
```
当运行以上代码时，你将会看到：

![舞台上的猫](/examples/images/screenshots/02.png)

我们正在取得一些进展！

如果你想从舞台中移除一个精灵，用 `removeChild` 方法：
```js
stage.removeChild(anySprite)
```
但是通常设置精灵的 `visible` 属性为 `false` 是一个让精灵消失的高效而且简单方式。
```js
anySprite.visible = false;
```
<a id='usingaliases'></a>
### 使用别名

你可以通过给Pixi对象和方法设置一个你经常用的简短的别名来使你的代码有更高的可读性。比如说， `PIXI.utils.TextureCache` 长不长？我认为长，特别是在一个大型项目你需要多次用到它。所以可以通过创建一个简短的别名指向它：
```js
var TextureCache = PIXI.utils.TextureCache
```
然后，用别名替换替换之前的位置：
```js
var texture = TextureCache["images/cat.png"];
```
除了让你能给更加简洁的代码，用别名还有一个好处：它有助于你缓存Pixi频繁变动的API。如果Pixi的API在将来的版本中改变了 - 一定会变！- 你仅仅需要在你的程序中更新你的别名，而不需要替换代码里所有的实例。所以当Pixi的开发团队决定重新调整的时候，你比他们还提前一步！

如何这么做，让我们重构刚才加载并展示图像的代码，给所有的Pixi对象和方法用别名。
```js
//Aliases
var Container = PIXI.Container,
    autoDetectRenderer = PIXI.autoDetectRenderer,
    loader = PIXI.loader,
    resources = PIXI.loader.resources,
    Sprite = PIXI.Sprite;

//Create a Pixi stage and renderer and add the 
//renderer.view to the DOM
var stage = new Container(),
    renderer = autoDetectRenderer(256, 256);
document.body.appendChild(renderer.view);

//load an image and run the `setup` function when it's done
loader
  .add("images/cat.png")
  .load(setup);

function setup() {

  //Create the `cat` sprite, add it to the stage, and render it
  var cat = new Sprite(resources["images/cat.png"].texture);  
  stage.addChild(cat);
  renderer.render(stage);
}

```
本教程中的大部分例子都将遵从这个相同的范式来为Pixi设置别名。除非另有说明，你可以假设所有的例子代码都会像这样一样使用别名。

这就是你需要加载图像和创建精灵的全部东西。

<a id='alittlemoreaboutloadingthings'></a>
### A little more about loading things

The format I've shown you above is what I suggest you use as your
standard template for loading images and displaying sprites. So, you
can safely ignore the next few paragraphs and jump straight to the
next section, "Positioning sprites." But Pixi's `loader` object is
quite sophisticated and includes a few features that you should be
aware of, even if you don't use them on a regular basis. Let's
look at some of the most useful.

<a id='makeaspritefromanordinaryjavascriptimageobject'></a>
#### Make a sprite from an ordinary JavaScript Image object or Canvas

For optimization and efficiency it’s always best to make a sprite from
a texture that’s been pre-loaded into Pixi’s texture cache. But if for
some reason you need to make a texture from a regular JavaScript
`Image`
object, you can do that using Pixi’s `BaseTexture` and `Texture`
classes:
```js
var base = new PIXI.BaseTexture(anyImageObject),
    texture = new PIXI.Texture(base),
    sprite = new PIXI.Sprite(texture);
```
You can use `BaseTexture.fromCanvas` if you want to make a texture
from any existing canvas element:
```js
var base = new PIXI.BaseTexture.fromCanvas(anyCanvasElement),
```
If you want to change the texture the sprite is displaying, use the
`texture` property. Set it to any `Texture` object, like this:
```js
anySprite.texture = PIXI.utils.TextureCache["anyTexture.png"];
```
You can use this technique to interactively change the sprite’s
appearance if something significant happens to it in the game.

<a id='assigninganametoaloadingfile'></a>
#### Assigning a name to a loading file

It's possible to assign a unique name to each resource you want to
load. Just supply the name (a string) as the first argument in the
`add` method. For example, here's how to name an image of a cat as
`catImage`.
```js
PIXI.loader
  .add("catImage", "images/cat.png")
  .load(setup);
```
This creates an object called `catImage` in `loader.resources`.
That means you can create a sprite by referencing the `catImage` object, like this:
```js
var cat = new PIXI.Sprite(PIXI.loader.resources.catImage.texture);
```
However, I recommend you don't use this feature! That's because you'll
have to remember all names you gave each loaded files, as well as make sure
you don't accidentally use the same name more than once. Using the file path name, as we've done in previous
examples is simpler and less error prone.

<a id='monitoringloadprogress'></a>
#### Monitoring load progress

Pixi's loader has a special `progress` event that will call a
customizable function that will run each time a file loads. `progress` events are called by the
`loader`'s `on` method, like this:
```js
PIXI.loader.on("progress", loadProgressHandler);
```
Here's how to include the `on` method in the loading chain, and call
a user-definable function called `loadProgressHandler` each time a file loads.
```js
PIXI.loader
  .add([
    "images/one.png",
    "images/two.png",
    "images/three.png"
  ])
  .on("progress", loadProgressHandler)
  .load(setup);

function loadProgressHandler() {
  console.log("loading"); 
}

function setup() {
  console.log("setup");
}
```
Each time one of the files loads, the progress event calls
`loadProgressHandler` to display "loading" in the console. When all three files have loaded, the `setup`
function will run. Here's the output of the above code in the console:
```js
loading
loading
loading
setup
```
That's neat, but it gets better. You can also find out exactly which file
has loaded and what percentage of overall files are have currently
loaded. You can do this by adding optional `loader` and
`resource` parameters to the `loadProgressHandler`, like this:
```js
function loadProgressHandler(loader, resource) { //...
```
You can then use `resource.url` to find the file that's currently
loaded. (Use `resource.name` if you want to find the optional name
that you might have assigned to the file, as the first argument in the
`add` method.) And you can use `loader.progress` to find what
percentage of total resources have currently loaded. Here's some code
that does just that.
```js
PIXI.loader
  .add([
    "images/one.png",
    "images/two.png",
    "images/three.png"
  ])
  .on("progress", loadProgressHandler)
  .load(setup);

function loadProgressHandler(loader, resource) {

  //Display the file `url` currently being loaded
  console.log("loading: " + resource.url); 

  //Display the precentage of files currently loaded
  console.log("progress: " + loader.progress + "%"); 

  //If you gave your files names as the first argument 
  //of the `add` method, you can access them like this
  //console.log("loading: " + resource.name);
}

function setup() {
  console.log("All files loaded");
}
```
Here's what this code will display in the console when it runs:
```js
loading: images/one.png
progress: 33.333333333333336%
loading: images/two.png
progress: 66.66666666666667%
loading: images/three.png
progress: 100%
All files loaded
```
That's really cool, because you could use this as the basis for
creating a loading progress bar. 

(Note: There are additional properties you can access on the
`resource` object. `resource.error` will tell you of any possible
error that happened while
trying to load a file. `resource.data` lets you
access the file's raw binary data.)

<a id='moreaboutpixisloader'></a>
#### More about Pixi's loader

Pixi's loader is ridiculously feature-rich and configurable. Let's
take a quick bird's-eye view of its usage to
get you started.

The loader's chainable `add` method takes 4 basic arguments:
```js
add(name, url, optionObject, callbackFunction)
```
Here's what the loader's source code documentation has to say about
these parameters:

`name` (string): The name of the resource to load. If it's not passed, the `url` is used.  
`url` (string): The url for this resource, relative to the `baseUrl` of the loader.  
`options` (object literal): The options for the load.  
`options.crossOrigin` (Boolean): Is the request cross-origin? The default is to determine automatically.  
`options.loadType`: How should the resource be loaded? The default value is `Resource.LOAD_TYPE.XHR`.  
`options.xhrType`: How should the data being loaded be interpreted
when using XHR? The default value is `Resource.XHR_RESPONSE_TYPE.DEFAULT`  
`callbackFunction`: The function to call when this specific resource completes loading.

The only one of these arguments that's required is the `url` (the file that you want to
load.) 

Here are some examples of some ways you could use the `add`
method to load files. These first ones are what the docs call the loader's "normal syntax":
```js
.add('key', 'http://...', function () {})
.add('http://...', function () {})
.add('http://...')
```
And these are examples of the loader's "object syntax":
```js
.add({
  name: 'key2',
  url: 'http://...'
}, function () {})

.add({
  url: 'http://...'
}, function () {})

.add({
  name: 'key3',
  url: 'http://...'
  onComplete: function () {}
})

.add({
  url: 'https://...',
  onComplete: function () {},
  crossOrigin: true
})
```
You can also pass the `add` method an array of objects, or urls, or
both:
```js
.add([
  {name: 'key4', url: 'http://...', onComplete: function () {} },
  {url: 'http://...', onComplete: function () {} },
  'http://...'
]);
```
(Note: If you ever need to reset the loader to load a new batch of files, call the
loader's `reset` method: `PIXI.loader.reset();`)

Pixi's loader has many more advanced features, including options to
let you load and parse binary files of all types. This is not
something you'll need to do on a day-to-day basis, and way outside the
scope of this tutorial, so [make sure to check out the loader's GitHub repository
for more information](https://github.com/englercj/resource-loader).

<a id='positioning'></a>
Positioning sprites
-------------------

Now that you know how to create and display sprites, let's find out
how to position and resize them.

In the earlier example the cat sprite was added to stage at
the top left corner. The cat has an `x` position of
0 and a `y` position of 0. You can change the position of the cat by
changing the values of its `x` and `y` properties. Here's how you can center the cat in the stage by
setting its `x` and `y` property values to 96.
```js
cat.x = 96;
cat.y = 96;
```
Add these two lines of code anywhere inside the `setup`
function, after you've created the sprite. 
```js
function setup() {

  //Create the `cat` sprite
  var cat = new Sprite(resources["images/cat.png"].texture);

  //Change the sprite's position
  cat.x = 96;
  cat.y = 96;

  //Add the cat to the stage so you can see it
  stage.addChild(cat);

  //Render the stage
  renderer.render(stage);
}
```
(Note: In this example,
`Sprite` is an alias for `PIXI.Sprite`, `TextureCache` is an
alias for `PIXI.utils.TextureCache`, and `resources` is an alias for
`PIXI.loader.resources` as described earlier. I'll be
using alias that follow this same format for all Pixi objects and
methods in the example code from now on.)

These two new lines of code will move the cat 96 pixels to the right,
and 96 pixels down. Here's the result:

![Cat centered on the stage](/examples/images/screenshots/03.png)

The cat's top left corner (its left ear) represents its `x` and `y`
anchor point. To make the cat move to the right, increase the
value of its `x` property. To make the cat move down, increase the
value of its `y` property. If the cat has an `x` value of 0, it will be at
the very left side of the stage. If it has a `y` value of 0, it will
be at the very top of the stage.

![Cat centered on the stage - diagram](/examples/images/screenshots/04.png)

Instead of setting the sprite's `x` and `y` properties independently,
you can set them together in a single line of code, like this:
```js
sprite.position.set(x, y)
```
<a id='sizenscale'></a>
Size and scale
--------------

You can change a sprite's size by setting its `width` and `height`
properties. Here's how to give the cat a `width` of 80 pixels and a `height` of
120 pixels.
```js
cat.width = 80;
cat.height = 120;
```
Add those two lines of code to the `setup` function, like this:
```js
function setup() {

  //Create the `cat` sprite
  var cat = new Sprite(resources["images/cat.png"].texture);

  //Change the sprite's position
  cat.x = 96;
  cat.y = 96;

  //Change the sprite's size
  cat.width = 80;
  cat.height = 120;

  //Add the cat to the stage so you can see it
  stage.addChild(cat);
}
```
Here's the result:

![Cat's height and width changed](/examples/images/screenshots/05.png)

You can see that the cat's position (its top left corner) didn't
change, only its width and height.

![Cat's height and width changed - diagram](/examples/images/screenshots/06.png)

Sprites also have `scale.x` and `scale.y` properties that change the
sprite's width and height proportionately. Here's how to set the cat's
scale to half size:
```js
cat.scale.x = 0.5;
cat.scale.y = 0.5;
```
Scale values are numbers between 0 and 1 that represent a
percentage of the sprite's size. 1 means 100% (full size), while
0.5 means 50% (half size). You can double the sprite's size by setting
its scale values to 2, like this:
```js
cat.scale.x = 2;
cat.scale.y = 2;
```
Pixi has an alternative, concise way for you set sprite's scale in one
line of code using the `scale.set` method.
```js
cat.scale.set(0.5, 0.5);
```
If that appeals to you, use it!

<a id='rotation'></a>
Rotation
--------

You can make a sprite rotate by setting its `rotation` property to a
value in [radians](http://www.mathsisfun.com/geometry/radians.html).
```js
cat.rotation = 0.5;
```
But around which point does that rotation happen?

You've seen that a sprite's top left corner represents its `x` and `y` position. That point is
called the **anchor point**. If you set the sprite’s `rotation`
property to something like `0.5`, the rotation will happen *around the
sprite’s anchor point*.
This diagram shows what effect this will have on our cat sprite.

![Rotation around anchor point - diagram](/examples/images/screenshots/07.png)

You can see that the anchor point, the cat’s left ear, is the center of the imaginary circle around which the cat is rotating.
What if you want the sprite to rotate around its center? Change the
sprite’s `anchor` point so that it’s centered inside the sprite, like
this:
```js
cat.anchor.x = 0.5;
cat.anchor.y = 0.5;
```
The `anchor.x` and `anchor.y` values represent a percentage of the texture’s dimensions, from 0 to 1 (0%
to 100%). Setting it to 0.5 centers the texture over the point. The location of the point
itself won’t change, just the way the texture is positioned over it.

This next diagram shows what happens to the rotated sprite if you center its anchor point.

![Rotation around centered anchor point - diagram](/examples/images/screenshots/08.png)

You can see that the sprite’s texture shifts up and to the left. This
is an important side-effect to remember!

Just like with `position` and `scale`, you can set the anchor’s x and
y values with one line of code like this:
```js
sprite.anchor.set(x, y)
```
Sprites also have a `pivot` property which works in a similar way to
`anchor`. `pivot` sets the position
of the sprite's x/y origin point. If you change the pivot point and
then rotate the sprite, it will
rotate around that origin point. For example, the following code will
set the sprite's `pivot.x` point to 32, and its `pivot.y` point to 32
```js
cat.pivot.set(32, 32)
```
Assuming that the sprite is 64x64 pixels, the sprite will now rotate
around its center point. But remember: if you change a sprite's pivot
point, you've also changed its x/y origin point. 

So, what's the difference between `anchor` and `pivot`? They're really
similar! `anchor` shifts the origin point of the sprite's image texture, using a 0 to 1 normalized value.
`pivot` shifts the origin of the sprite's x and y point, using pixel
values. Which should you use? It's up to you. Just play around
with both of them and see which you prefer.

<a id='tileset'></a>
Make a sprite from a tileset sub-image
--------------------------------------

You now know how to make a sprite from a single image file. But, as a
game designer, you’ll usually be making your sprites using
**tilesets** (also known as **spritesheets**.) Pixi has some convenient built-in ways to help you do this.
A tileset is a single image file that contains sub-images. The sub-images
represent all the graphics you want to use in your game. Here's an
example of a tileset image that contains game characters and game
objects as sub-images.

![An example tileset](/examples/images/screenshots/09.png)

The entire tileset is 192 by 192 pixels. Each image is in a its own 32 by 32
pixel grid cell. Storing and accessing all your game graphics on a
tileset is a very
processor and memory efficient way to work with graphics, and Pixi is
optimized for them.

You can capture a sub-image from a tileset by defining a rectangular
area
that's the same size and position as the sub-image you want to
extract. Here's an example of the rocket sub-image that’s been extracted from
the tileset.

![Rocket extracted from tileset](/examples/images/screenshots/10.png)

Let's look at the code that does this. First, load the `tileset.png` image
with Pixi’s `loader`, just as you've done in earlier examples.
```js
loader
  .add("images/tileset.png")
  .load(setup);
```
Next, when the image has loaded, use a rectangular sub-section of the tileset to create the
sprite’s image. Here's the code that extracts the sub image, creates
the rocket sprite, and positions and displays it on the canvas.
```js
function setup() {

  //Create the `tileset` sprite from the texture
  var texture = TextureCache["images/tileset.png"];

  //Create a rectangle object that defines the position and
  //size of the sub-image you want to extract from the texture
  var rectangle = new Rectangle(192, 128, 64, 64);

  //Tell the texture to use that rectangular section
  texture.frame = rectangle;

  //Create the sprite from the texture
  var rocket = new Sprite(texture);

  //Position the rocket sprite on the canvas
  rocket.x = 32;
  rocket.y = 32;

  //Add the rocket to the stage
  stage.addChild(rocket);
  
  //Render the stage   
  renderer.render(stage);
}
```
How does this work?

Pixi has a built-in `Rectangle` object (PIXI.Rectangle) that is a general-purpose
object for defining rectangular shapes. It takes four arguments. The
first two arguments define the rectangle's `x` and `y` position. The
last two define its `width` and `height`. Here's the format
for defining a new `Rectangle` object.
```js
var rectangle = new PIXI.Rectangle(x, y, width, height);
```
The rectangle object is just a *data object*; it's up to you to decide how you want to use it. In
our example we're using it to define the position and area of the
sub-image on the tileset that we want to extract. Pixi textures have a useful
property called `frame` that can be set to any `Rectangle` objects. 
The `frame` crops the texture to the dimensions of the `Rectangle`.
Here's how to use `frame`
to crop the texture to the size and position of the rocket.
```js
var rectangle = new Rectangle(192, 128, 64, 64);
texture.frame = rectangle;
```
You can then use that cropped texture to create the sprite:
```js
var rocket = new Sprite(texture);
```
And that's how it works!

Because making sprite textures from a tileset
is something you’ll do with great frequency, Pixi has a more convenient way
to help you do this - let's find out what that is next.

<a id='textureatlas'></a>
Using a texture atlas
---------------------

If you’re working on a big, complex game, you’ll want a fast and
efficient way to create sprites from tilesets. This is where a
**texture atlas** becomes really useful. A texture atlas is a JSON
data file that contains the positions and sizes of sub-images on a
matching tileset PNG image. If you use a texture atlas, all you need
to know about the sub-image you want to display is its name. You
can arrange your tileset images in any order and the JSON file
will keep track of their sizes and positions for you. This is
really convenient because it means the sizes and positions of
tileset images aren’t hard-coded into your game program. If you
make changes to the tileset, like adding images, resizing them,
or removing them, just re-publish the JSON file and your game will
use that data to display the correct images. You won’t have to
make any changes to your game code.

Pixi is compatible with a standard JSON texture atlas format that is
output by a popular software tool called [Texture
Packer](https://www.codeandweb.com/texturepacker). Texture Packer’s
“Essential” license is free. Let’s find out how to use it to make a
texture atlas, and load the atlas into Pixi. (You don’t have to use
Texture Packer. Similar tools, like [Shoebox](http://renderhjs.net/shoebox/) or [spritesheet.js](https://github.com/krzysztof-o/spritesheet.js/), output PNG and JSON files
in a standard format that is compatible with Pixi.)

First, start with a collection of individual image files that you'd
like to use in your game.

![Image files](/examples/images/screenshots/11.png)

(All the images in this section were created by Lanea Zimmerman. You
can find more of her artwork
[here](http://opengameart.org/users/sharm).
Thanks, Lanea!)

Next, open Texture Packer and choose **JSON Hash** as the framework
type. Drag your images into Texture Packer's workspace. (You can
also point Texture Packer to any folder that contains your images.)
It will automatically arrange the images on a single tileset image, and give them names that match their original image names.

![Image files](/examples/images/screenshots/12.png)

(If you're using the free version of
Texture Packer, set **Algorithm** to `Basic`, set **Trim mode** to
`None`, set **Size constraints** to `Any size` and slide the **PNG Opt
Level** all the way to the left to `0`. These are the basic
settings that will allow the free version of Texture Packer to create
your files without any warnings or errors.)

When you’re done, click the **Publish** button. Choose the file name and
location, and save the published files. You’ll end up with 2 files: a
PNG file and a JSON file. In this example my file names are
`treasureHunter.json` and `treasureHunter.png`. To make your life easier,
just keep both files in your project’s `images` folder. (You can think
of the JSON file as extra metadata for the image file, so it makes
sense to keep both files in the same folder.)
The JSON file describes the name, size and position of each of the
sub-images
in the tileset. Here’s an excerpt that describes the blob monster
sub-image.
```js
"blob.png":
{
	"frame": {"x":55,"y":2,"w":32,"h":24},
	"rotated": false,
	"trimmed": false,
	"spriteSourceSize": {"x":0,"y":0,"w":32,"h":24},
	"sourceSize": {"w":32,"h":24},
	"pivot": {"x":0.5,"y":0.5}
},
```
The `treasureHunter.json` file also contains “dungeon.png”,
“door.png”, "exit.png", and "explorer.png" properties each with
similar data. Each of these sub-images are called **frames**. Having
this data is really helpful because now you don’t need to know the
size and position of each sub-image in the tileset. All you need to
know is the sprite’s **frame id**. The frame id is just the name
of the original image file, like "blob.png" or "explorer.png".

Among the many advantages to using a texture atlas is that you can
easily add 2 pixels of padding around each image (Texture Packer does
this by default.) This is important to prevent the possibility of
**texture bleed**. Texture bleed is an effect that happens when the
edge of an adjacent image on the tileset appears next to a sprite.
This happens because of the way your computer's GPU (Graphics
Processing Unit) decides how to round fractional pixels values. Should
it round them up or down? This will be different for each GPU.
Leaving 1 or 2 pixels spacing around images on a tilseset makes all
images display consistently.

(Note: If you have two pixels of padding around a graphic, and you still notice a strange "off by one pixel" glitch in the
way Pixi is displaying it, try changing the texture's scale mode
algorithm. Here's how: `texture.baseTexture.scaleMode =
PIXI.SCALE_MODES.NEAREST;`. These glitches can sometimes happen
because of GPU floating point rounding errors.)

Now that you know how to create a texture atlas, let's find out how to
load it into your game code.

<a id='loadingatlas'></a>
Loading the texture atlas
-------------------------

To get the texture atlas into Pixi, load it using Pixi’s
`loader`. If the JSON file was made with Texture Packer, the
`loader` will interpret the data and create a texture from each
frame on the tileset automatically.  Here’s how to use the `loader` to load the `treasureHunter.json`
file. When it has loaded, the `setup` function will run.
```js
loader
  .add("images/treasureHunter.json")
  .load(setup);
```
Each image on the tileset is now an individual texture in Pixi’s
cache. You can access each texture in the cache with the same name it
had in Texture Packer (“blob.png”, “dungeon.png”, “explorer.png”,
etc.).

<a id='creatingsprites'></a>
Creating sprites from a loaded texture atlas
--------------------------------------------

Pixi gives you three general ways to create a sprite from a texture atlas:

1.	Using `TextureCache`:
```js
var texture = TextureCache["frameId.png"],
    sprite = new Sprite(texture);
```
2.	If you’ve used Pixi’s `loader` to load the texture atlas, use the 
loader’s `resources`:
```js
var sprite = new Sprite(
  resources["images/treasureHunter.json"].textures["frameId.png"]
);
```
3. That’s way too much typing to do just to create a sprite! 
So I suggest you create an alias called `id` that points to texture’s 
altas’s `textures` object, like this:
```js
var id = PIXI.loader.resources["images/treasureHunter.json"].textures; 
```
Then you can just create each new sprite like this:
```js
let sprite = new Sprite(id["frameId.png"]);
```
Much better!

Here's how you could use these three different sprite creation
techniques in the `setup` function to create and display the
`dungeon`, `explorer`, and `treasure` sprites.
```js
//Define variables that might be used in more 
//than one function
var dungeon, explorer, treasure, door, id;

function setup() {

  //There are 3 ways to make sprites from textures atlas frames

  //1. Access the `TextureCache` directly
  var dungeonTexture = TextureCache["dungeon.png"];
  dungeon = new Sprite(dungeonTexture);
  stage.addChild(dungeon);

  //2. Access the texture using the loader's `resources`:
  explorer = new Sprite(
    resources["images/treasureHunter.json"].textures["explorer.png"]
  );
  explorer.x = 68;

  //Center the explorer vertically
  explorer.y = stage.height / 2 - explorer.height / 2;
  stage.addChild(explorer);

  //3. Create an optional alias called `id` for all the texture atlas 
  //frame id textures.
  id = PIXI.loader.resources["images/treasureHunter.json"].textures; 
  
  //Make the treasure box using the alias
  treasure = new Sprite(id["treasure.png"]);
  stage.addChild(treasure);

  //Position the treasure next to the right edge of the canvas
  treasure.x = stage.width - treasure.width - 48;
  treasure.y = stage.height / 2 - treasure.height / 2;
  stage.addChild(treasure);


  //Render the stage
  renderer.render(stage);
}
```
Here's what this code displays:

![Explorer, dungeon and treasure](/examples/images/screenshots/13.png)

The stage dimensions are 512 by 512 pixels, and you can see in the
code above that the `stage.height` and `stage.width` properties are used
to align the sprites. Here's how the `explorer`'s `y` position is
vertically centered:
```js
explorer.y = stage.height / 2 - explorer.height / 2;
```
Learning to create and display sprites using a texture atlas is an
important benchmark. So before we continue, let's take a look at the
code you
could write to add the remaining
sprites: the `blob`s and `exit` door, so that you can produce a scene
that looks like this:

![All the texture atlas sprites](/examples/images/screenshots/14.png)

Here's the entire code that does all this. I've also included the HTML
code so you can see everything in its proper context.
(You'll find this working code in the
`examples/spriteFromTextureAtlas.html` file in this repository.)
Notice that the `blob` sprites are created and added to the stage in a
loop, and assigned random positions.
```js
<!doctype html>
<meta charset="utf-8">
<title>Make a sprite from a texture atlas</title>
<body>
<script src="../pixi.js/bin/pixi.js"></script>
<script>

//Aliases
var Container = PIXI.Container,
    autoDetectRenderer = PIXI.autoDetectRenderer,
    loader = PIXI.loader,
    resources = PIXI.loader.resources,
    TextureCache = PIXI.utils.TextureCache,
    Texture = PIXI.Texture,
    Sprite = PIXI.Sprite;

//Create a Pixi stage and renderer and add the 
//renderer.view to the DOM
var stage = new Container(),
    renderer = autoDetectRenderer(512, 512);
document.body.appendChild(renderer.view);

//load a JSON file and run the `setup` function when it's done
loader
  .add("images/treasureHunter.json")
  .load(setup);

//Define variables that might be used in more 
//than one function
var dungeon, explorer, treasure, door, id;

function setup() {

  //There are 3 ways to make sprites from textures atlas frames

  //1. Access the `TextureCache` directly
  var dungeonTexture = TextureCache["dungeon.png"];
  dungeon = new Sprite(dungeonTexture);
  stage.addChild(dungeon);

  //2. Access the texture using throuhg the loader's `resources`:
  explorer = new Sprite(
    resources["images/treasureHunter.json"].textures["explorer.png"]
  );
  explorer.x = 68;

  //Center the explorer vertically
  explorer.y = stage.height / 2 - explorer.height / 2;
  stage.addChild(explorer);

  //3. Create an optional alias called `id` for all the texture atlas 
  //frame id textures.
  id = PIXI.loader.resources["images/treasureHunter.json"].textures; 
  
  //Make the treasure box using the alias
  treasure = new Sprite(id["treasure.png"]);
  stage.addChild(treasure);

  //Position the treasure next to the right edge of the canvas
  treasure.x = stage.width - treasure.width - 48;
  treasure.y = stage.height / 2 - treasure.height / 2;
  stage.addChild(treasure);

  //Make the exit door
  door = new Sprite(id["door.png"]); 
  door.position.set(32, 0);
  stage.addChild(door);

  //Make the blobs
  var numberOfBlobs = 6,
      spacing = 48,
      xOffset = 150;

  //Make as many blobs as there are `numberOfBlobs`
  for (var i = 0; i < numberOfBlobs; i++) {

    //Make a blob
    var blob = new Sprite(id["blob.png"]);

    //Space each blob horizontally according to the `spacing` value.
    //`xOffset` determines the point from the left of the screen
    //at which the first blob should be added.
    var x = spacing * i + xOffset;

    //Give the blob a random y position
    //(`randomInt` is a custom function - see below)
    var y = randomInt(0, stage.height - blob.height);

    //Set the blob's position
    blob.x = x;
    blob.y = y;

    //Add the blob sprite to the stage
    stage.addChild(blob);
  }

  //Render the stage   
  renderer.render(stage);
}

//The `randomInt` helper function
function randomInt(min, max) {
  return Math.floor(Math.random() * (max - min + 1)) + min;
}

</script>
</body>
```
You can see in the code above that all the blobs are created using a
`for` loop. Each `blob` is spaced evenly along the `x` axis like this:
```js
var x = spacing * i + xOffset;
blob.x = x;
```
`spacing` has a value 48, and `xOffset` has a value of 150. What this
means is the first `blob` will have an `x` position of 150.
This offsets it from the left side of the stage by 150 pixel. Each
subsequent `blob` will have an `x` value that's 48 pixels greater than
the `blob` created in the previous iteration of the loop. This creates
an evenly spaced line of blob monsters, from left to right, along the dungeon floor.

Each `blob` is also given a random `y` position. Here's the code that
does this:
```js
var y = randomInt(0, stage.height - blob.height);
blob.y = y;
```
The `blob`'s `y` position could be assigned any random number between 0 and
512, which is the value of `stage.height`. This works with the help of
a custom function called `randomInt`. `randomInt` returns a random number
that's within a range between any two numbers you supply.
```js
randomInt(lowestNumber, highestNumber)
```
That means if you want a random number between 1 and 10, you can get
one like this:
```js
var randomNumber = randomInt(1, 10);
```
Here's the `randomInt` function definition that does all this work:
```js
function randomInt(min, max) {
  return Math.floor(Math.random() * (max - min + 1)) + min;
}
```
`randomInt` is a great little function to keep in your back pocket for
making games - I use it all the time.

<a id='movingsprites'></a>
Moving Sprites
--------------

You now know how to display sprites, but how do you make them move?
That's easy: create a looping function using `requestAnimationFrame`.
This is called a **game loop**.
Any code you put inside the game loop will update 60 times per
second. Here's some code you could write to make the `cat` sprite move
at a rate  of 1 pixel per frame.
```js
function gameLoop() {

  //Loop this function at 60 frames per second
  requestAnimationFrame(gameLoop);

  //Move the cat 1 pixel to the right each frame
  cat.x += 1;

  //Render the stage to see the animation
  renderer.render(stage);
}

//Start the game loop
gameLoop();
```
If you run this bit of code, you'll see the sprite gradually move to
the right side of the stage.

![Moving sprites](/examples/images/screenshots/15.png)

And that's really all there is to it! Just change any sprite property by small
increments inside the loop, and they'll animate over time. If you want
the sprite to animate in the opposite direction (to the left), just give it a
negative value, like `-1`.
You'll find this code in the `movingSprites.html` file - here's the
complete code:
```js
//Aliases
var Container = PIXI.Container,
    autoDetectRenderer = PIXI.autoDetectRenderer,
    loader = PIXI.loader,
    resources = PIXI.loader.resources,
    Sprite = PIXI.Sprite;

//Create a Pixi stage and renderer 
var stage = new Container(),
    renderer = autoDetectRenderer(256, 256);
document.body.appendChild(renderer.view);

//Load an image and the run the `setup` function
loader
  .add("images/cat.png")
  .load(setup);

//Define any variables that are used in more than one function
var cat;

function setup() {

  //Create the `cat` sprite 
  cat = new Sprite(resources["images/cat.png"].texture);
  cat.y = 96; 
  stage.addChild(cat);
 
  //Start the game loop
  gameLoop();
}

function gameLoop(){

  //Loop this function 60 times per second
  requestAnimationFrame(gameLoop);

  //Move the cat 1 pixel per frame
  cat.x += 1;

  //Render the stage
  renderer.render(stage);
}
```
(Notice that the `cat` variable needs to be defined outside the
`setup` and
`gameLoop` functions so that you can access it inside both of them.)

You can animate a sprite's scale, rotation, or size - whatever! You'll see
many more examples of how to animate sprites ahead.

<a id='velocity'></a>
Using velocity properties
-------------------------

To give you more flexibility, its a good idea to control a sprite's
movement speed using two **velocity properties**: `vx` and `vy`. `vx`
is used to set the sprite's speed and direction on the x axis
(horizontally). `vy` is
used to set the sprite's speed and direction on the y axis (vertically). Instead of
changing a sprite's `x` and `y` values directly, first update the velocity
variables, and then assign those velocity values to the sprite. This is an
extra bit of modularity that you'll need for interactive game animation.

The first step is to create `vx` and `vy` properties on your sprite,
and give them an initial value.
```js
cat.vx = 0;
cat.vy = 0;
```
Setting `vx` and `vy` to 0 means that the sprite isn't moving.

Next, in the game loop, update `vx` and `vy` with the velocity
that you want the sprite to move at. Then assign those values to the
sprite's `x` and `y` properties. Here's how you could use this
technique to make the cat sprite move down and to right at one pixel each
frame:
```js
function setup() {

  //Create the `cat` sprite 
  cat = new Sprite(resources["images/cat.png"].texture);
  stage.addChild(cat);

  //Initialize the cat's velocity variables
  cat.vx = 0;
  cat.vy = 0;
 
  //Start the game loop
  gameLoop();
}

function gameLoop(){

  //Loop this function 60 times per second
  requestAnimationFrame(gameLoop);

  //Update the cat's velocity
  cat.vx = 1;
  cat.vy = 1;

  //Apply the velocity values to the cat's 
  //position to make it move
  cat.x += cat.vx;
  cat.y += cat.vy;

  //Render the stage
  renderer.render(stage);
}


```
When you run this code, the cat will move down and to the right at one
pixel per frame:

![Moving sprites](/examples/images/screenshots/16.png)

What if you want to make the cat move in a different direction? To
make the cat move to the left, give it a `vx` value of `-1`. To make
it move up, give the cat a `vy` value of `-1`. To make the cat move
faster, give it larger `vx` and `vy` values, like `3`, `5`, `-2`, or
`-4`.

You'll see ahead how modularizing a sprite's velocity with `vx` and
`vy` velocity properties helps with keyboard and mouse pointer
control systems for games, as well as making it easier to implement physics.

<a id='gamestates'></a>
Game states
-----------

As a matter of style, and to help modularize your code, I
recommend structuring your game loop like this:
```js
//Set the game's current state to `play`:
var state = play;

function gameLoop() {

  //Loop this function at 60 frames per second
  requestAnimationFrame(gameLoop);

  //Update the current game state:
  state();

  //Render the stage to see the animation
  renderer.render(stage);
}

function play() {

  //Move the cat 1 pixel to the right each frame
  cat.x += 1;
}
```
You can see that the `gameLoop` is calling a function called `state` 60 times
per second. What is the `state` function? It's been assigned to
`play`. That means all the code in the `play` function will also run at 60
times per second.

Here's how the code from the previous example can be re-factored to
this new model:
```js
//Define any variables that are used in more than one function
var cat, state;

function setup() {

  //Create the `cat` sprite 
  cat = new Sprite(resources["images/cat.png"].texture);
  cat.y = 96; 
  cat.vx = 0;
  cat.vy = 0;
  stage.addChild(cat);

  //Set the game state
  state = play;
 
  //Start the game loop
  gameLoop();
}

function gameLoop(){

  //Loop this function 60 times per second
  requestAnimationFrame(gameLoop);

  //Update the current game state:
  state();

  //Render the stage
  renderer.render(stage);
}

function play() {

  //Move the cat 1 pixel to the right each frame
  cat.vx = 1
  cat.x += cat.vx;
}
```
Yes, I know, this is a bit of [head-swirler](http://www.amazon.com/Electric-Psychedelic-Sitar-Headswirlers-1-5/dp/B004HZ14VS)! But, don't let it scare
and you and spend a minute or two walking through in your mind how those
functions are connected. As you'll see ahead, structuring your game
loop like this will make it much, much easier to do things like switching
game scenes and levels.

<a id='keyboard'></a>
Keyboard Movement
-----------------

With just a little more work you can build a simple system to control
a sprite using the keyboard. To simplify your code, I suggest you use
this custom function called `keyboard` that listens for and captures
keyboard events.
```js
function keyboard(keyCode) {
  var key = {};
  key.code = keyCode;
  key.isDown = false;
  key.isUp = true;
  key.press = undefined;
  key.release = undefined;
  //The `downHandler`
  key.downHandler = function(event) {
    if (event.keyCode === key.code) {
      if (key.isUp && key.press) key.press();
      key.isDown = true;
      key.isUp = false;
    }
    event.preventDefault();
  };

  //The `upHandler`
  key.upHandler = function(event) {
    if (event.keyCode === key.code) {
      if (key.isDown && key.release) key.release();
      key.isDown = false;
      key.isUp = true;
    }
    event.preventDefault();
  };

  //Attach event listeners
  window.addEventListener(
    "keydown", key.downHandler.bind(key), false
  );
  window.addEventListener(
    "keyup", key.upHandler.bind(key), false
  );
  return key;
}
```
The `keyboard` function is easy to use. Create a new keyboard object like this:
```js
var keyObject = keyboard(asciiKeyCodeNumber);
```
It's one argument is the ASCII key code number of the keyboad key that you
want to listen for.
[Here's a list of ASCII keyboard code
numbers](http://help.adobe.com/en_US/AS2LCR/Flash_10.0/help.html?content=00000520.html).

Then assign `press` and `release` methods to the keyboard object like this:
```js
keyObject.press = function() {
  //key object pressed
};
keyObject.release = function() {
  //key object released
};
```
Keyboard objects also have `isDown` and `isUp` Boolean properties that
you can use to check the state of each key.

Take a look at the
`keyboardMovement.html` file in the `examples` folder to see how you
can use this `keyboard` function to control a sprite using your
keyboard's arrow keys. Run it and use the left, up, down, and right
arrow keys to move the cat around the stage.

![Keyboard movement](/examples/images/screenshots/17.png)

Here's the code that does all this:
```js
function setup() {

  //Create the `cat` sprite
  cat = new Sprite("images/cat.png");
  cat.y = 96;
  cat.vx = 0;
  cat.vy = 0;
  stage.addChild(cat);

  //Capture the keyboard arrow keys
  var left = keyboard(37),
      up = keyboard(38),
      right = keyboard(39),
      down = keyboard(40);

  //Left arrow key `press` method
  left.press = function() {

    //Change the cat's velocity when the key is pressed
    cat.vx = -5;
    cat.vy = 0;
  };

  //Left arrow key `release` method
  left.release = function() {

    //If the left arrow has been released, and the right arrow isn't down,
    //and the cat isn't moving vertically:
    //Stop the cat
    if (!right.isDown && cat.vy === 0) {
      cat.vx = 0;
    }
  };

  //Up
  up.press = function() {
    cat.vy = -5;
    cat.vx = 0;
  };
  up.release = function() {
    if (!down.isDown && cat.vx === 0) {
      cat.vy = 0;
    }
  };

  //Right
  right.press = function() {
    cat.vx = 5;
    cat.vy = 0;
  };
  right.release = function() {
    if (!left.isDown && cat.vy === 0) {
      cat.vx = 0;
    }
  };

  //Down
  down.press = function() {
    cat.vy = 5;
    cat.vx = 0;
  };
  down.release = function() {
    if (!up.isDown && cat.vx === 0) {
      cat.vy = 0;
    }
  };

  //Set the game state
  state = play;

  //Start the game loop
  gameLoop();
}

function gameLoop() {
  requestAnimationFrame(gameLoop);
  state();
  renderer.render(stage);
}

function play() {

  //Use the cat's velocity to make it move
  cat.x += cat.vx;
  cat.y += cat.vy
}
```
<a id='grouping'></a>
Grouping Sprites
----------------

Groups let you create game scenes, and manage similar sprites together
as single units. Pixi has an object called a `Container`
that lets you do this. Let's find out how it works.

Imagine that you want to display three sprites: a cat, hedgehog and
tiger. Create them, and set their positions - *but don't add them to the
stage*.
```js
//The cat
var cat = new Sprite(id["cat.png"]);
cat.position.set(16, 16);

//The hedgehog
var hedgehog = new Sprite(id["hedgehog.png"]);
hedgehog.position.set(32, 32);

//The tiger
var tiger = new Sprite(id["tiger.png"]);
tiger.position.set(64, 64);
```

Next, create an `animals` container to group them all together like
this:
```js
var animals = new Container();
```
Then use `addChild` to *add the sprites to the group*.
```js
animals.addChild(cat);
animals.addChild(hedgehog);
animals.addChild(tiger);
```
Finally add the group to the stage.
```js
stage.addChild(animals);
renderer.render(stage);
```
(As you know, the `stage` object is also a `Container`. It’s the root
container for all Pixi sprites.)

Here's what this code produces:

![Grouping sprites](/examples/images/screenshots/18.png)

What you can't see in that image is the invisible `animals` group
that's containing the sprites.

![Grouping sprites](/examples/images/screenshots/19.png)

You can now treat the `animals` group as a single unit. You can think
of a `Container` as a special kind of sprite that doesn’t
have a texture.

If you need a list of all the child sprites that `animals` contains,
use its `children` array to find out.
```
console.log(animals.children)
//Displays: Array [Object, Object, Object]
```
This tells you that `animals` has three sprites as children.

Because the `animals` group is just like any other sprite, you can
change its `x` and `y` values, `alpha`, `scale` and
all the other sprite properties. Any property value you change on the
parent container will affect the child sprites in a relative way. So if you
set the group's `x` and `y` position, all the child sprites will
be repositioned relative to the group's top left corner. What would
happen if you set the `animals`'s `x` and `y` position to 64?
```
animals.position.set(64, 64);
```
The whole group of sprites will move 64 pixels right and 64 pixels to
the down.

![Grouping sprites](/examples/images/screenshots/20.png)

The `animals` group also has its own dimensions, which is based on the area
occupied by the containing sprites. You can find its `width` and
`height` values like this:
```js
console.log(animals.width);
//Displays: 112

console.log(animals.height);
//Displays: 112

```
![Group width and height](/examples/images/screenshots/21.png)

What happens if you change a group's width or height?
```js
animals.width = 200;
animals.height = 200;
```
All the child
sprites will scale to match that change.

![Group width and height](/examples/images/screenshots/22.png)

You can nest as many `Container`s inside other
`Container`s as you like, to create deep hierarchies if
you need to. However, a `DisplayObject` (like a `Sprite` or another
`Container`) can only belong to one parent at a time. If
you use `addChild` to make a sprite the child of another object, Pixi
will automatically remove it from its current parent. That’s a useful
bit of management that you don’t have to worry about.

<a id='localnglobal'></a>
### Local and global positions

When you add a sprite to a `Container`, its `x` and `y`
position is *relative to the group’s top left corner*. That's the
sprite's **local position** For example, what do you think the cat's
position is in this image?

![Grouping sprites](/examples/images/screenshots/20.png)

Let's find out:
```
console.log(cat.x);
//Displays: 16
```
16? Yes! That's because the cat is offset by only 16 pixel's from the
group's top left corner. 16 is the cat's local position.

Sprites also have a **global position**. The global position is the
distance from the top left corner of the stage, to the sprite's anchor
point (usually the sprite's top left corner.) You can find a sprite's global
position with the help of the `toGlobal` method.  Here's how:
```
parentSprite.toGlobal(childSprite.position)
```
That means you can find the cat's global position inside the `animals`
group like this:
```
console.log(animals.toGlobal(cat.position));
//Displays: Object {x: 80, y: 80...};
```
That gives you an `x` and `y` position of 80. That's exactly the cat's
global position relative to the top left corner of the stage. 

What if you want to find the global position of a sprite, but don't
know what the sprite's parent container
is? Every sprite has a property called `parent` that will tell you what the
sprite's parent is. If you add a sprite directly to the `stage`, then
`stage` will be the sprite's parent. In the example above, the `cat`'s
parent is `animals`. That means you can alternatively get the cat's global position
by writing code like this:
```
cat.parent.toGlobal(cat.position);
```
And it will work even if you don't know what the cat's parent
container currently is.

There's one more way to calculate the global position! And, it's
actually the best way, so heads up! If you want to know the distance
from the top left corner of the canvas to the sprite, and don't know
or care what the sprite's parent containers are, use the
`getGlobalPosition` method. Here's how to use it to find the tiger's global position:
```js
tiger.getGlobalPosition().x
tiger.getGlobalPosition().y
```
This will give you `x` and `y` values of 128 in the example that we've
been using.
The special thing about `getGlobalPosition` is that it's highly
precise: it will give you the sprite's accurate global position as
soon as its local position changes. I asked the Pixi development team
to add this feature specifically for accurate collision detection for
games.

What if you want to convert a global position to a local position? you
can use the `toLocal` method. It works in a similar way, but uses this
general format:
```js
sprite.toLocal(sprite.position, anyOtherSprite)
```
Use `toLocal` to find the distance between a sprite and any other
sprite. Here's how you could find out the tiger's local
position, relative to the hedgehog.
```js
tiger.toLocal(tiger.position, hedgehog).x
tiger.toLocal(tiger.position, hedgehog).y
```
This gives you an `x` value of 32 and a `y` value of 32. You can see
in the example images that the tiger's top left corner is 32 pixels
down and to the left of the hedgehog's top left corner.

<a id='spritebatch'></a>
### Using a ParticleContainer to group sprites

Pixi has an alternative, high-performance way to group sprites called
a `ParticleContainer` (`PIXI.ParticleContainer`). Any sprites inside a
`ParticleContainer` will render 2 to 5
times faster than they would if they were in a regular
`Container`. It’s a great performance boost for games.

Create a `ParticleContainer` like this:
```js
var superFastSprites = new ParticleContainer();
```
Then use `addChild` to add sprites to it, just like you would with any
ordinary `Container`.

You have to make some compromises if you decide to use a
`ParticleContainer`. Sprites inside a `ParticleContainer` only have a few  basic properties:
`x`, `y`, `width`, `height`, `scale`, `pivot`, `alpha`, `visible` – and that’s
about it. Also, the sprites that it contains can’t have nested
children of their own. A `ParticleContainer` also can’t use Pixi’s advanced
visual effects like filters and blend modes. Each `ParticleContainer` can use only one texture (so you'll have to use a spritesheet if you want Sprites with different appearances). But for the huge performance boost that you get, those
compromises are usually worth it. And you can use
`Container`s and `ParticleContainer`s simultaneously in the same project, so you can fine-tune your optimization.

Why are sprites in a `Particle Container` so fast? Because the positions of
the sprites are being calculated directly on the GPU. The Pixi
development team is working to offload as much sprite processing as
possible on the GPU, so it’s likely that the latest version of Pixi
that you’re using will have much more feature-rich `ParticleContainer` than
what I've described here. Check the current [`ParticleContainer`
documentation](http://pixijs.download/release/docs/PIXI.particles.ParticleContainer.html) for details.

Where you create a `ParticleContainer`, there are two optional
arguments you can provide: the maximum number of sprites the container
can hold, and an options object.
```js
var superFastSprites = new ParticleContainer(size, options);
```
The default value for size is 15,000. So, if you need to contain more
sprites, set it to a higher number. The options argument is an object
with 5 Boolean values you can set: `scale`, `position`, `rotation`, `uvs` and
`alpha`. The default value of `position` is `true`, but all the others
are set to `false`. That means that if you want change the `rotation`,
`scale`, `alpha`, or `uvs` of sprite in the `ParticleContainer`, you
have to set those properties to `true`, like this:
```js
var superFastSprites = new ParticleContainer(
  size, 
  {
    rotation: true,
    alpha: true,
    scale: true,
    uvs: true
  }
);
```
But, if you don't think you'll need to use these properties, keep them
set to `false` to squeeze out the maximum amount of performance.

What's the `uvs` option? Only set it to `true` if you have particles
which change their textures while they're being animated. (All the
sprite's textures will also need to be on the same tileset image for
this to work.) 

(Note: **UV mapping** is a 3D graphics display term that refers to
the `x` and `y` coordinates of the texture (the image) that is being
mapped onto a 3D surface. `U` is the `x` axis and `V` is the `y` axis.
WebGL already uses `x`, `y` and `z` for 3D spatial positioning, so `U`
and `V` were chosen to represent `x` and `y` for 2D image textures.)

<a id='graphic'></a>
Pixi's Graphic Primitives
-------------------------

Using image textures is one of the most useful ways of making sprites,
but Pixi also has its own low-level drawing tools. You can use them to
make rectangles, shapes, lines, complex polygons and text. And,
fortunately, it uses almost the same API as the [Canvas Drawing API](https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API/Drawing_graphics_with_canvas) so,
if you're already familiar with canvas, here’s nothing really new to
  learn. But the big advantage is that, unlike the Canvas Drawing API,
  the shapes you draw with Pixi are rendered by WebGL on the GPU. Pixi
  lets you access all that untapped performance power.
Let’s take a quick tour of how to make some basic shapes. Here are all
the shapes we'll make in the code ahead.

![Graphic primitives](/examples/images/screenshots/23.png)

<a id='rectangles'></a>
### Rectangles

All shapes are made by first creating a new instance of Pixi's
`Graphics` class (`PIXI.Graphics`).
```js
var rectangle = new Graphics();
```
Use `beginFill` with a hexadecimal color code value to set the
rectangle’ s fill color. Here’ how to set to it to light blue.
```js
rectangle.beginFill(0x66CCFF);
```
If you want to give the shape an outline, use the `lineStyle` method. Here's
how to give the rectangle a 4 pixel wide red outline, with an `alpha`
value of 1.
```js
rectangle.lineStyle(4, 0xFF3300, 1);
```
Use the `drawRect` method to draw the rectangle. Its four arguments
are `x`, `y`, `width` and `height`.
```js
rectangle.drawRect(x, y, width, height);
```
Use `endFill` when you’re done.
```js
rectangle.endFill();
```
It’s just like the Canvas Drawing API! Here’s all the code you need to
draw a rectangle, change its position, and add it to the stage.
```js
var rectangle = new Graphics();
rectangle.lineStyle(4, 0xFF3300, 1);
rectangle.beginFill(0x66CCFF);
rectangle.drawRect(0, 0, 64, 64);
rectangle.endFill();
rectangle.x = 170;
rectangle.y = 170;
stage.addChild(rectangle);

```
This code makes a 64 by 64 blue rectangle with a red border at an x and y position of 170.

<a id='circles'></a>
### Circles

Make a circle with the `drawCircle` method. Its three arguments are
`x`, `y` and `radius`
```js
drawCircle(x, y, radius)
```
Unlike rectangles and sprites, a circle’s x and y position is also its
center point. Here’s how to make a violet colored circle with a radius of 32 pixels.
```js
var circle = new Graphics();
circle.beginFill(0x9966FF);
circle.drawCircle(0, 0, 32);
circle.endFill();
circle.x = 64;
circle.y = 130;
stage.addChild(circle);
```
<a id='ellipses'></a>
### Ellipses
As a one-up on the Canvas Drawing API, Pixi lets you draw an ellipse
with the `drawEllipse` method.
```js
drawEllipse(x, y, width, height);
```
The x/y position defines the ellipse’s top left corner (imagine that
the ellipse is surrounded by an invisible rectangular bounding box -
the top left corner of that box will represent the ellipse's x/y
anchor position). Here’s a yellow ellipse that’s 50 pixels wide and 20 pixels high.
```js
var ellipse = new Graphics();
ellipse.beginFill(0xFFFF00);
ellipse.drawEllipse(0, 0, 50, 20);
ellipse.endFill();
ellipse.x = 180;
ellipse.y = 130;
stage.addChild(ellipse);
```
<a id='roundedrect'></a>
### Rounded rectangles

Pixi also lets you make rounded rectangles with the `drawRoundedRect`
method. The last argument, `cornerRadius` is a number in pixels that
determines by how much the corners should be rounded.
```js
drawRoundedRect(x, y, width, height, cornerRadius)
```
Here's how to make a rounded rectangle with a corner radius of 10
pixels.
```js
var roundBox = new Graphics();
roundBox.lineStyle(4, 0x99CCFF, 1);
roundBox.beginFill(0xFF9933);
roundBox.drawRoundedRect(0, 0, 84, 36, 10)
roundBox.endFill();
roundBox.x = 48;
roundBox.y = 190;
stage.addChild(roundBox);
```
<a id='lines'></a>
### Lines

You've seen in the examples above that the `lineStyle` method lets you
define a line.  You can use the `moveTo` and `lineTo` methods to draw the
start and end points of the line, in just the same way you can with the Canvas
Drawing API. Here’s how to draw a 4 pixel wide, white diagonal line.
```js
var line = new Graphics();
line.lineStyle(4, 0xFFFFFF, 1);
line.moveTo(0, 0);
line.lineTo(80, 50);
line.x = 32;
line.y = 32;
stage.addChild(line);
```
`PIXI.Graphics` objects, like lines, have `x` and `y` values, just
like sprites, so you can position them anywhere on the stage after
you've drawn them.

<a id='polygons'></a>
### Polygons

You can join lines together and fill them with colors to make complex
shapes using the `drawPolygon` method. `drawPolygon`'s argument is an
path array of x/y points that define the positions of each point on the
shape.
```js
var path = [
  point1X, point1Y,
  point2X, point2Y,
  point3X, point3Y
];

graphicsObject.drawPolygon(path);
```
`drawPolygon` will join those three points together to make the shape.
Here’s how to use `drawPolygon` to connect three lines together to
make a red triangle with a blue border. The triangle is drawn at
position 0,0 and then moved to its position on the stage using its
`x` and `y` properties.
```js
var triangle = new Graphics();
triangle.beginFill(0x66FF33);

//Use `drawPolygon` to define the triangle as
//a path array of x/y positions

triangle.drawPolygon([
    -32, 64,             //First point
    32, 64,              //Second point
    0, 0                 //Third point
]);

//Fill shape's color
triangle.endFill();

//Position the triangle after you've drawn it.
//The triangle's x/y position is anchored to its first point in the path
triangle.x = 180;
triangle.y = 22;

stage.addChild(triangle);
```
<a id='text'></a>
Displaying text
---------------

Use a `Text` object (`PIXI.Text`) to display text on the stage. The constructor
takes two arguments: the text you want to display and a style object
that defines the font’s properties. Here's how to display the words
"Hello Pixi", in white, 32 pixel high Arial font.
```js
var message = new Text(
  "Hello Pixi!",
  {fontFamily: "Arial", fontSize: 32, fill: "white"}
);

message.position.set(54, 96);
stage.addChild(message);
```
![Displaying text](/examples/images/screenshots/24.png)

Pixi’s Text objects inherit from the `Sprite` class, so they
contain all the same properties like `x`, `y`, `width`, `height`,
`alpha`, and `rotation`. Position and resize text on the stage just like you would any other sprite.

If you want to change the content of a text object after you've
created it, use the `text` property.
```js
message.text = "Text changed!";
```
Use the `style` property if you want to redefine the font properties.
```js
message.style = {fill: "black", font: "16px PetMe64"};
```
Pixi makes text objects by using the Canvas Drawing API to
render the text to an invisible and temporary canvas
element. It then turns the canvas into a WebGL texture so that it
can be mapped onto a sprite. That’s why the text’s color needs to be
wrapped in a string: it’s a Canvas Drawing API color value. As with
any canvas color values, you can use words for common colors like
“red” or “green”, or use rgba, hsla or hex values.

Other style properties that you can include are `stroke` for the font
outline color and `strokeThickness` for the outline thickness. Set the
text's `dropShadow` property to `true` to make the text display a
shadow. Use `dropShadowColor` to set the shadow's hexadecimal color
value, use `dropShadowAngle` to set the shadow's angle in radians, and
use `dropShadowDistance` to set the pixel height of a shadow. And
there's more: [check out Pixi's Text documentation for the full
list](http://pixijs.download/release/docs/PIXI.Text.html).

Pixi can also wrap long lines of text. Set the text’s `wordWrap` style
property to `true`, and then set `wordWrapWidth` to the maximum length
in pixels, that the line of text should be. Use the `align` property
to set the alignment for multi-line text.
```js
message.style = {wordWrap: true, wordWrapWidth: 100, align: center};
```
(Note: `align` doesn't affect single line text.)

If you want to use a custom font file, use the CSS `@font-face` rule
to link the font file to the HTML page where your Pixi application is
running.
```js
@font-face {
  font-family: "fontFamilyName";
  src: url("fonts/fontFile.ttf");
}
```
Add this `@font-face` rule to your HTML page's CSS style sheet.

[Pixi also has support for bitmap
fonts](http://pixijs.download/release/docs/PIXI.extras.BitmapText.html). You
can use Pixi's loader to load Bitmap font XML files, the same way you
load JSON or image files.

<a id='collision'></a>
Collision detection
--------------------------

You now know how to make a huge variety of graphics objects, but what
can you do with them? A fun thing to do is to build a simple **collision
detection** system. You can use a custom function called
`hitTestRectangle` that checks whether any two rectangular Pixi sprites are
touching.
```js
hitTestRectangle(spriteOne, spriteTwo)
```
if they overlap, `hitTestRectangle` will return `true`. You can use `hitTestRectangle` with an `if` statement to check for a collision between two sprites like this:
```js
if (hitTestRectangle(cat, box)) {
  //There's a collision
} else {
  //There's no collision
}
```
As you'll see, `hitTestRectangle` is the front door into the vast universe of game design.

Run the `collisionDetection.html` file in the `examples` folder for a
working example of how to use `hitTestRectangle`. Use the arrow keys
to move the cat. If the cat hits the box, the box becomes red
and "Hit!" is displayed by the text object.

![Displaying text](/examples/images/screenshots/25.png)

You've already seen all the code that creates all these elements, as
well as the
keyboard control system that makes the cat move. The only new thing is the
way `hitTestRectangle` is used inside the `play` function to check for a
collision.
```js
function play() {

  //use the cat's velocity to make it move
  cat.x += cat.vx;
  cat.y += cat.vy;

  //check for a collision between the cat and the box
  if (hitTestRectangle(cat, box)) {

    //if there's a collision, change the message text
    //and tint the box red
    message.text = "hit!";
    box.tint = 0xff3300;

  } else {

    //if there's no collision, reset the message
    //text and the box's color
    message.text = "No collision...";
    box.tint = 0xccff99;
  }
}
```
Because the `play` function is being called by the game loop 60 times
per second, this `if` statement is constantly checking for a collision
between the cat and the box. If `hitTestRectangle` is `true`, the
text `message` object uses `setText` to display "Hit":
```js
message.text = "hit!";
```
The color of the box is then changed from green to red by setting the
box's `tint` property to the hexadecimal red value.
```js
box.tint = 0xff3300;
```
If there's no collision, the message and box are maintained in their
original states:
```js
message.text = "no collision...";
box.tint = 0xccff99;
```
This code is pretty simple, but suddenly you've created an interactive
world that seems to be completely alive. It's almost like magic! And, perhaps
surprisingly, you now have all the skills you need to start making
games with Pixi!

<a id='hittest'></a>
### The hitTestRectangle function

But what about the `hitTestRectangle` function? What does it do, and
how does it work? The details of how collision detection algorithms
like this work is a little bit outside the scope of this tutorial.
The most important thing is that you know how to use it. But, just for
your reference, and in case you're curious, here's the complete
`hitTestRectangle` function definition. Can you figure out from the
comments what it's doing?
```js
function hitTestRectangle(r1, r2) {

  //Define the variables we'll need to calculate
  var hit, combinedHalfWidths, combinedHalfHeights, vx, vy;

  //hit will determine whether there's a collision
  hit = false;

  //Find the center points of each sprite
  r1.centerX = r1.x + r1.width / 2;
  r1.centerY = r1.y + r1.height / 2;
  r2.centerX = r2.x + r2.width / 2;
  r2.centerY = r2.y + r2.height / 2;

  //Find the half-widths and half-heights of each sprite
  r1.halfWidth = r1.width / 2;
  r1.halfHeight = r1.height / 2;
  r2.halfWidth = r2.width / 2;
  r2.halfHeight = r2.height / 2;

  //Calculate the distance vector between the sprites
  vx = r1.centerX - r2.centerX;
  vy = r1.centerY - r2.centerY;

  //Figure out the combined half-widths and half-heights
  combinedHalfWidths = r1.halfWidth + r2.halfWidth;
  combinedHalfHeights = r1.halfHeight + r2.halfHeight;

  //Check for a collision on the x axis
  if (Math.abs(vx) < combinedHalfWidths) {

    //A collision might be occuring. Check for a collision on the y axis
    if (Math.abs(vy) < combinedHalfHeights) {

      //There's definitely a collision happening
      hit = true;
    } else {

      //There's no collision on the y axis
      hit = false;
    }
  } else {

    //There's no collision on the x axis
    hit = false;
  }

  //`hit` will be either `true` or `false`
  return hit;
};

```
<a id='casestudy'></a>
Case study: Treasure Hunter
---------------

So I told you that you now have all the skills you need to start
making games. What? You don't believe me? Let me prove it to you! Let’s take a
close at how to make a simple object collection and enemy
avoidance game called **Treasure Hunter**. (You'll find it the `examples`
folder.)

![Treasure Hunter](/examples/images/screenshots/26.png)

Treasure Hunter is a good example of one of simplest complete
games you can make using the tools you've learnt so far. Use the
keyboard arrow
keys to help the explorer find the treasure and carry it to the exit.
Six blob monsters move up and down between the dungeon walls, and if
they hit the explorer he becomes semi-transparent and the health meter
at the top right corner shrinks. If all the health is used up, “You
Lost!” is displayed on the stage; if the explorer reaches the exit with
the treasure, “You Won!” is displayed. Although it’s a basic
prototype, Treasure Hunter contains most of the elements you’ll find
in much bigger games: texture atlas graphics, interactivity,
collision, and multiple game scenes. Let’s go on a tour of how the
game was put together so that you can use it as a starting point for one of your own games.

### The code structure

Open the `treasureHunter.html` file and you'll see that all the game
code is in one big file. Here's a birds-eye view of how all the code is
organized.

```js
//Setup Pixi and load the texture atlas files - call the `setup`
//function when they've loaded

function setup() {
  //Initialize the game sprites, set the game `state` to `play`
  //and start the 'gameLoop'
}

function gameLoop() {
  //Runs the current game `state` in a loop and renders the sprites
}

function play() {
  //All the game logic goes here
}

function end() {
  //All the code that should run at the end of the game
}

//The game's helper functions:
//`keyboard`, `hitTestRectangle`, `contain` and `randomInt`
```
Use this as your world map to the game as we look at how each
section works.

<a id='initialize'></a>
### Initialize the game in the setup function

As soon as the texture atlas images have loaded, the `setup` function
runs. It only runs once, and lets you perform
one-time setup tasks for your game. It's a great place to create and initialize
objects, sprites, game scenes, populate data arrays or parse
loaded JSON game data.

Here's an abridged view of the `setup` function in Treasure Hunter,
and the tasks that it performs.

```js
function setup() {
  //Create the `gameScene` group
  //Create the `door` sprite
  //Create the `player` sprite
  //Create the `treasure` sprite
  //Make the enemies
  //Create the health bar
  //Add some text for the game over message
  //Create a `gameOverScene` group
  //Assign the player's keyboard controllers

  //set the game state to `play`
  state = play;

  //Start the game loop
  gameLoop();
}

```
The last two lines of code, `state = play;` and `gameLoop()` are perhaps
the most important. Running `gameLoop` switches on the game's engine,
and causes the `play` function to be called in a continuous loop. But before we look at how that works, let's see what the
specific code inside the `setup` function does.

<a id='gamescene'></a>
#### Creating the game scenes

The `setup` function creates two `Container` groups called
`gameScene` and `gameOverScene`. Each of these are added to the stage.
```js
gameScene = new Container();
stage.addChild(gameScene);

gameOverScene = new Container();
stage.addChild(gameOverScene);

```
All of the sprites that are part of the main game are added to the
`gameScene` group. The game over text that should be displayed at the
end of the game is added to the `gameOverScene` group.

![Displaying text](/examples/images/screenshots/27.png)

Although it's created in the `setup` function, the `gameOverScene`
shouldn't be visible when the game first starts, so its `visible`
property is initialized to `false`.
```js
gameOverScene.visible = false;
```
You'll see ahead that, when the game ends, the `gameOverScene`'s `visible`
property will be set to `true` to display the text that appears at the
end of the game.

<a id='makingdungon'></a>
#### Making the dungeon, door, explorer and treasure

The player, exit door, treasure chest and the dungeon background image
are all sprites made from texture atlas frames. Very importantly,
they're all added as children of the `gameScene`.
```js
//Create an alias for the texture atlas frame ids
id = resources["images/treasureHunter.json"].textures;

//Dungeon
dungeon = new Sprite(id["dungeon.png"]);
gameScene.addChild(dungeon);

//Door
door = new Sprite(id["door.png"]);
door.position.set(32, 0);
gameScene.addChild(door);

//Explorer
explorer = new Sprite(id["explorer.png"]);
explorer.x = 68;
explorer.y = gameScene.height / 2 - explorer.height / 2;
explorer.vx = 0;
explorer.vy = 0;
gameScene.addChild(explorer);

//Treasure
treasure = new Sprite(id["treasure.png"]);
treasure.x = gameScene.width - treasure.width - 48;
treasure.y = gameScene.height / 2 - treasure.height / 2;
gameScene.addChild(treasure);
```
Keeping them together in the `gameScene` group will make it easy for
us to hide the `gameScene` and display the `gameOverScene` when the game is finished.

<a id='makingblob'></a>
#### Making the blob monsters

The six blob monsters are created in a loop. Each blob is given a
random initial position and velocity. The vertical velocity is
alternately multiplied by `1` or `-1` for each blob, and that’s what
causes each blob to move in the opposite direction to the one next to
it. Each blob monster that's created is pushed into an array called
`blobs`.
```js
var numberOfBlobs = 6,
    spacing = 48,
    xOffset = 150,
    speed = 2,
    direction = 1;

//An array to store all the blob monsters
blobs = [];

//Make as many blobs as there are `numberOfBlobs`
for (var i = 0; i < numberOfBlobs; i++) {

  //Make a blob
  var blob = new Sprite(id["blob.png"]);

  //Space each blob horizontally according to the `spacing` value.
  //`xOffset` determines the point from the left of the screen
  //at which the first blob should be added
  var x = spacing * i + xOffset;

  //Give the blob a random `y` position
  var y = randomInt(0, stage.height - blob.height);

  //Set the blob's position
  blob.x = x;
  blob.y = y;

  //Set the blob's vertical velocity. `direction` will be either `1` or
  //`-1`. `1` means the enemy will move down and `-1` means the blob will
  //move up. Multiplying `direction` by `speed` determines the blob's
  //vertical direction
  blob.vy = speed * direction;

  //Reverse the direction for the next blob
  direction *= -1;

  //Push the blob into the `blobs` array
  blobs.push(blob);

  //Add the blob to the `gameScene`
  gameScene.addChild(blob);
}

```
<a id='healthbar'></a>
#### Making the health bar

When you play Treasure Hunter you'll notice that when the explorer touches
one of the enemies, the width of the health bar at the top right
corner of the screen decreases. How was this health bar made? It's
just two overlapping rectangles at exactly the same position: a black rectangle behind, and
a red rectangle in front. They're grouped into a single `healthBar`
group. The `healthBar` is then added to the `gameScene` and positioned
on the stage.
```js
//Create the health bar
healthBar = new PIXI.DisplayObjectContainer();
healthBar.position.set(stage.width - 170, 6)
gameScene.addChild(healthBar);

//Create the black background rectangle
var innerBar = new PIXI.Graphics();
innerBar.beginFill(0x000000);
innerBar.drawRect(0, 0, 128, 8);
innerBar.endFill();
healthBar.addChild(innerBar);

//Create the front red rectangle
var outerBar = new PIXI.Graphics();
outerBar.beginFill(0xFF3300);
outerBar.drawRect(0, 0, 128, 8);
outerBar.endFill();
healthBar.addChild(outerBar);

healthBar.outer = outerBar;
```
You can see that a property called `outer` has been added to the
`healthBar`. It just references the `outerBar` (the red rectangle) so that it will be convenient to access later.
```js
healthBar.outer = outerBar;
```
You don't have to do this; but, hey why not! It means that if you want
to control the width of the red `outerBar`, you can write some smooth code that looks like this:
```js
healthBar.outer.width = 30;
```
That's pretty neat and readable, so we'll keep it!

<a id='message'></a>
#### Making the message text

When the game is finished, some text displays “You won!” or “You
lost!”, depending on the outcome of the game. This is made using a
text sprite and adding it to the `gameOverScene`. Because the
`gameOverScene`‘s `visible` property is set to `false` when the game
starts, you can’t see this text. Here’s the code from the `setup`
function that creates the message text and adds it to the
`gameOverScene`.
```js
message = new Text(
  "The End!",
  {font: "64px Futura", fill: "white"}
);

message.x = 120;
message.y = stage.height / 2 - 32;

gameOverScene.addChild(message);
```
<a id='playing'></a>
### Playing the game

All the game logic and the code that makes the sprites move happens
inside the `play` function, which runs in a continuous loop. Here's an
overview of what the `play` function does
```js
function play() {
  //Move the explorer and contain it inside the dungeon
  //Move the blob monsters
  //Check for a collision between the blobs and the explorer
  //Check for a collision between the explorer and the treasure
  //Check for a collsion between the treasure and the door
  //Decide whether the game has been won or lost
  //Change the game `state` to `end` when the game is finsihed
}
```
Let's find out how all these features work.

<a id='movingexplorer'></a>
### Moving the explorer

The explorer is controlled using the keyboard, and the code that does
that is very similar to the keyboard control code you learnt earlier.
The `keyboard` objects modify the explorer’s velocity, and that
velocity is added to the explorer’s position inside the `play`
function.
```js
explorer.x += explorer.vx;
explorer.y += explorer.vy;
```
<a id='containingmovement'></a>
#### Containing movement

But what's new is that the explorer's movement is contained inside the walls of the
dungeon. The green outline shows the limits of the explorer's
movement.

![Displaying text](/examples/images/screenshots/28.png)

That's done with the help of a custom function called
`contain`.
```js
contain(explorer, {x: 28, y: 10, width: 488, height: 480});
```
`contain` takes two arguments. The first is the sprite you want to keep
contained. The second is any object with `x`, `y`, `width` and
`height` properties that define a rectangular area. In this example,
the containing object defines an area that's just slightly offset
from, and smaller than, the stage. It matches dimensions of the dungeon
walls.

Here's the `contain` function that does all this work. The function checks
to see if the sprite has crossed the boundaries of the containing
object. If it has, the code moves the sprite back into that boundary.
The `contain` function also returns a `collision` variable with the
value "top", "right", "bottom" or "left", depending on which side of
the boundary the sprite hit. (`collision` will be `undefined` if the
sprite didn't hit any of the boundaries.)
```js
function contain(sprite, container) {

  var collision = undefined;

  //Left
  if (sprite.x < container.x) {
    sprite.x = container.x;
    collision = "left";
  }

  //Top
  if (sprite.y < container.y) {
    sprite.y = container.y;
    collision = "top";
  }

  //Right
  if (sprite.x + sprite.width > container.width) {
    sprite.x = container.width - sprite.width;
    collision = "right";
  }

  //Bottom
  if (sprite.y + sprite.height > container.height) {
    sprite.y = container.height - sprite.height;
    collision = "bottom";
  }

  //Return the `collision` value
  return collision;
}
```
You'll see how the `collision` return value will be use in the code
ahead to make the blob monsters bounce back and forth between the top
and bottom dungeon walls.

<a id='movingmonsters'></a>
### Moving the monsters

The `play` function also moves the blob monsters, keeps them contained
inside the dungeon walls, and checks each one for a collision with the
player. If a blob bumps into the dungeon’s top or bottom walls, its
direction is reversed. All this is done with the help of a `forEach` loop
which iterates through each of `blob` sprites in the `blobs` array on
every frame.
```js
blobs.forEach(function(blob) {

  //Move the blob
  blob.y += blob.vy;

  //Check the blob's screen boundaries
  var blobHitsWall = contain(blob, {x: 28, y: 10, width: 488, height: 480});

  //If the blob hits the top or bottom of the stage, reverse
  //its direction
  if (blobHitsWall === "top" || blobHitsWall === "bottom") {
    blob.vy *= -1;
  }

  //Test for a collision. If any of the enemies are touching
  //the explorer, set `explorerHit` to `true`
  if(hitTestRectangle(explorer, blob)) {
    explorerHit = true;
  }
});

```
You can see in this code above how the return value of the `contain`
function is used to make the blobs bounce off the walls. A variable
called `blobHitsWall` is used to capture the return value:
```js
var blobHitsWall = contain(blob, {x: 28, y: 10, width: 488, height: 480});
```
`blobHitsWall` will usually be `undefined`. But if the blob hits the
top wall, `blobHitsWall` will have the value "top". If the blob hits
the bottom wall, `blobHitsWall` will have the value "bottom". If
either of these cases are `true`, you can reverse the blob's direction
by reversing its velocity. Here's the code that does this:
```js
if (blobHitsWall === "top" || blobHitsWall === "bottom") {
  blob.vy *= -1;
}
```
Multiplying the blob's `vy` (vertical velocity) value by `-1` will flip
the direction of its movement.

<a id='checkingcollisions'></a>
### Checking for collisions

The code in the loop above uses `hitTestRectangle` to figure
out if any of the enemies have touched the explorer.
```js
if(hitTestRectangle(explorer, blob)) {
  explorerHit = true;
}
```
If `hitTestRectangle` returns `true`, it means there’s been a collision
and a variable called `explorerHit` is set to `true`. If `explorerHit`
is `true`, the `play` function makes the explorer semi-transparent
and reduces the width of the `health` bar by 1 pixel.
```js
if(explorerHit) {

  //Make the explorer semi-transparent
  explorer.alpha = 0.5;

  //Reduce the width of the health bar's inner rectangle by 1 pixel
  healthBar.outer.width -= 1;

} else {

  //Make the explorer fully opaque (non-transparent) if it hasn't been hit
  explorer.alpha = 1;
}

```
If  `explorerHit` is `false`, the explorer's `alpha` property is
maintained at 1, which makes it fully opaque.

The `play` function also checks for a collision between the treasure
chest and the explorer. If there’s a hit, the `treasure` is set to the
explorer’s position, with a slight offset. This makes it look like the
explorer is carrying the treasure.

![Displaying text](/examples/images/screenshots/29.png)

Here's the code that does this:

```js
if (hitTestRectangle(explorer, treasure)) {
  treasure.x = explorer.x + 8;
  treasure.y = explorer.y + 8;
}
```
<a id='reachingexit'></a>
### Reaching the exit door and ending the game

There are two ways the game can end: You can win if you carry the
treasure to the exit, or you can lose if you run out of health.

To win the game, the treasure chest just needs to touch the exit door. If
that happens, the game `state` is set to `end`, and the `message` text
displays "You won".
```js
if (hitTestRectangle(treasure, door)) {
  state = end;
  message.text = "You won!";
}
```
If you run out of health, you lose the game. The game `state` is also
set to `end` and the `message` text displays "You Lost!"
```js
if (healthBar.outer.width < 0) {
  state = end;
  message.text = "You lost!";
}
```
But what does this mean?
```js
state = end;
```
You'll remember from earlier examples that the `gameLoop` is constantly updating a function called
`state` at 60 times per second. Here's the `gameLoop`that does this:
```js
function gameLoop(){

  //Loop this function 60 times per second
  requestAnimationFrame(gameLoop);

  //Update the current game state
  state();

  //Render the stage
  renderer.render(stage);
}
```
You'll also remember that we initially set the value of
`state` to `play`, which is why the `play` function runs in a loop.
By setting `state` to `end` we're telling the code that we want
another function, called `end` to run in a loop. In a bigger game you
could have a `tileScene` state, and states for each game level, like
`leveOne`, `levelTwo` and `levelThree`.

So what is that `end` function? Here it is!
```js
function end() {
  gameScene.visible = false;
  gameOverScene.visible = true;
}
```
It just flips the visibility of the game scenes. This is what hides
the `gameScene` and displays the `gameOverScene` when the game ends.

This is a really simple example of how to switch a game's state, but
you can have as many game states as you like in your games, and fill them
with as much code as you need. Just change the value of `state` to
whatever function you want to run in a loop.

And that’s really all there is to Treasure Hunter! With a little more work you could turn this simple prototype into a full game – try it!

<a id='spriteproperties'></a>
More about sprites
-----------------------------

You've learnt how to use quite a few useful sprite properties so far, like `x`, `y`,
`visible`, and `rotation` that give you a lot of control over a
sprite's position and appearance. But Pixi Sprites also have many more
useful properties that are fun to play with. [Here's the full list.](http://pixijs.download/release/docs/PIXI.Sprite.html)

How does Pixi’s class inheritance system work? ([What is a **class**
and what is **inheritence**? Click this link to find out.](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Introduction_to_Object-Oriented_JavaScript)) Pixi’s sprites are
built on an inheritance model that follows this chain:
```
DisplayObject > Container > Sprite
```
Inheritance just means that the classes later in the chain use
properties and methods from classes earlier in the chain.
The most basic class is `DisplayObject`. Anything that’s a
`DisplayObject` can be rendered on the stage. `Container`
is the next class in the inheritance chain. It allows `DisplayObject`s
to act as containers for other `DisplayObject`s. Third up the chain is
the `Sprite` class. That’s the class you’ll be using to make most of
your game objects. However, later you’ll learn how to use
`Container`s to group sprites together.

<a id='takingitfurther'></a>
Taking it further
-----------------

Pixi can do a lot, but it can't do everything! If you want to start
making games or complex interactive applications with Pixi, you'll need
to use some helper libraries:

- [Bump](https://github.com/kittykatattack/bump): A complete suite of 2D collision functions for games.
- [Tink](https://github.com/kittykatattack/tink): Drag-and-drop, buttons, a universal pointer and other
  helpful interactivity tools.
- [Charm](https://github.com/kittykatattack/charm): Easy-to-use tweening animation effects for Pixi sprites.
- [Dust](https://github.com/kittykatattack/dust): Particle effects for creating things like explosions, fire
  and magic.
- [Sprite Utilities](https://github.com/kittykatattack/spriteUtilities): Easier and more intuitive ways to
  create and use Pixi sprites, as well adding a state machine and
  animation player. Makes working with Pixi a lot more fun.
- [Sound.js](https://github.com/kittykatattack/sound.js): A micro-library for loading, controlling and generating
  sound and music effects. Everything you need to add sound to games.
- [Smoothie](https://github.com/kittykatattack/smoothie): Ultra-smooth sprite animation using true delta-time interpolation. It also lets you specify the fps (frames-per-second) at which your game or application runs, and completely separates your sprite rendering loop from your application logic loop.

You can find out how to use all these libraries with Pixi in the book 
[Learn PixiJS](http://www.springer.com/us/book/9781484210956).

<a id='hexi'></a>
### Hexi

Do you want to use all the functionality of those libraries, but don't
want the hassle of integrating them yourself? Use **Hexi**: a complete
development environment for building games and interactive
applications:

https://github.com/kittykatattack/hexi

It bundles the best version of Pixi (the latest stable one) with all these 
libraries (and more!) for a simple and fun way to make games. Hexi also
lets you access the global `PIXI` object directly, so you can write
low-level Pixi code directly in a Hexi application, and optionally choose to use as many or
as few of Hexi's extra conveniences as you need.

<a id='supportingthisproject'></a>
Please help to support this project!
-------------------

Buy the book! Incredibly, someone actually paid me to finish writing this tutorial
and turn it into a book! 

[Learn PixiJS](http://www.springer.com/us/book/9781484210956)

(And it's not just some junky "e-book", but a real, heavy, paper book, published by Springer,
the world's largest publisher! That means you can invite your friends
over, set it on fire, and roast marshmallows!!) There's 80% more
content than what's in this tutorial, and it's
packed full of all the essential techniques you need to know to use
Pixi to make all kinds of interactive applications and games.

Find out how to:

- Make animated game characters.
- Create a full-featured animation state player.
- Dynamically animate lines and shapes.
- Use tiling sprites for infinite parallax scrolling.
- Use blend modes, filters, tinting, masks, video, and render textures.
- Produce content for multiple resolutions.
- Create interactive buttons.
- Create a flexible drag and drop interface for Pixi.
- Create particle effects.
- Build a stable software architectural model that will scale to any size.
- Make complete games.

And, as a bonus, all the code is written entirely in the latest version of
JavaScript: ES6/2015.

If you want to support this project, please buy a copy of this book,
and buy another copy for your mom!

