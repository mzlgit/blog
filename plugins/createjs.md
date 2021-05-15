### createJs
> CreateJS是基于HTML5开发的一套模块化的库和工具。
> 基于这些库，可以非常快捷地开发出基于HTML5的游戏、动画和交互应用。

#### preload-js
> PreloadJS是一个用来管理和协调相关资源加载的类库，
> 它可以方便的帮助你预先加载相关资源。

PreloadJS便于预先加载资源：图像、声音、数据、或其他的JS。

它采用xhr2提供真正的进展信息可用时，或回落到标签加载和缓和的进步时，它不是。它允许多个队列，队列的多个连接，暂停，和更多。
```js
安装 preload-js

npm i -S preload-js

//其他npm包无法正常 import 引入插件
```

+ 实例
``` js
var queue = new createjs.LoadQueue();
 queue.installPlugin(createjs.Sound);
 queue.on("complete", handleComplete, this);
 queue.loadFile({id:"sound", src:"http://path/to/sound.mp3"});
 queue.loadManifest([
     {id: "myImage", src:"path/to/myImage.jpg"}
 ]);
 function handleComplete() {
     createjs.Sound.play("sound");
     var image = queue.getResult("myImage");
     document.body.appendChild(image);
 }
```

+ 项目中使用
```js
//引入插件 
import createjs from "preload-js"
// 加载的资源 项目中使用到的静态资源
let pathList = [
    require("@/assets/43.jpg"),
    require("@/assets/56.jpg"),
    require("@/assets/99.jpg"),
    require("@/assets/bg-4.png"),
    require("@/assets/bg-cover-3.png"),
    require("@/assets/bg-cover-31.png"),
    require("@/assets/bg-cover-32.png"),
    require("@/assets/logo-name.png"),
    require("@/assets/season.png"),
]
// 加载函数
loading() {
    // 实例化
    let queue = new createjs.LoadQueue();
    // 指定完成加载后的回调
    queue.on("complete", this.handleComplete, this);
    // 进度过程回调
    queue.on("progress", this.handleProgress, this);
    // 错误回调
    queue.on("error", this.handleError, this);
    // 加载资源
    queue.loadManifest(this.pathList);
},
handleComplete(){
    // 完成加载
    console.log(122)
},
handleError(err){
    console.log(err)
},
handleProgress(event){
    // 进度反馈
    console.log(321, event.progress)
}
```

+ 在项目的过程中，如果使用了部分资源放置在 static 文件夹中，路径需要为： ./static/...
  + 例如，放置了svga动画资源（test.svga），需要使用 preload-js 加载资源，直接使用路径为 “./static/svga/test.svga”，然后加载即可。