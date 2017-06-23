## webpack 的延伸 02 :blush:

咦咦咦，你还看着👀呢！欢迎👏接着看我的这个webpack系列--**webpack的延伸2**。在上一篇的文章中，自己主要是实现了下面的这三个功能：

- 实现es6语法的支持

- 处理css

- 整合less

如果你对这三个不是很熟练的话，虽然本文档的接下来的学习影响可以忽略不计，但是还是建议你回头看下[webpack_extend01](./webpack_extend01.md)。

**提示** -- 本文档实现的项目的是在项目--[webpack_demo_extend01](./webpack_demo_extend01/)的基础上实现的。

下面我们将来学习--

1.加载图片

在没有实现的之前，我修改了下一下文件`src/index.less`，内容如下

```less

body{
    background:url('https://ss1.bdstatic.com/70cFvXSh_Q1YnxGkpoWK1HF6hhy/it/u=1510363862,3286190187&fm=26&gp=0.jpg') no-repeat;
    p{
        color:red;
    }
}

```

其他的是些标识性的文案的小改动，这里不贴出来。

在改动之口，我执行`npm run dev`之后，得到浏览器的截图如下：

![starry sky](./assets/imgs/starry_sky.jpg)

咦，很神奇，是吧，背景图已经导进去了啊，拿还讲个啥。可以，你留意到`background:url('https://ss1.bdstatic.com/70cFvXSh_Q1YnxGkpoWK1HF6hhy/it/u=1510363862,3286190187&fm=26&gp=0.jpg') no-repeat;`，它的url是一个cdn的链接。如果换成本地的图片链接会怎样呢？

我在根目录下新建了一个文件夹`assets`,在此文件夹下面新建`images`文件夹，再在此文件夹下面添加自己找的图片`webpack_image.jpeg`。那么，我直接替换掉相关的`background里面的url为background:url('../assets/images/webpack_image.jpeg')就行了呢`？答案是不行的。如果怀疑，你可以下载本文档相关的项目--[webpack_demo_extend02](./webpack_demo_extend02/)来修改运行一下了咯。

要实现本地的图片的资源下载的话，就需要使用到`file-loader`加载器。下面实现一下这个加图片--

1.1安装相关的依赖 'file-loader'

进入根目录，在控制台上面执行`npm install --save-dev file-loader`

1.2添加处理规则

 进入`webpack.config.dev.js`中，修改`module`字段如下：

 ```javascript

    ...
    module:{
        rules:[
            {// 处理js-es6的规则
                test:/\.js$/,//处理的文件的后缀名
                use:['babel-loader'],//处理的加载器是loader
                include:path.join(__dirname,'src')//包含的路径
            },
            {//处理css的规则,处理less的规则
                test:/\.less$/,
                use:[
                    {loader:'style-loader'},//style-loader 和 css-loader 的顺序是不能够颠倒的
                    {
                        loader:'css-loader',
                        // options:{
                        //     modules:true
                        // }
                    },
                    {loader:'autoprefixer-loader'},
                    {loader:'less-loader'},
                ]
            },
            {//处理图片资源
                test:/\.(png|svg|jpg|jpeg|gif)$/,//这里处理了以.png .svg .jpg .jpeg .gif为后缀名的图片
                use:[
                    {loader:'file-loader'}
                ]
            }
        ]
    }
    ...

 ```

 完成上面的两个步骤之后，执行`npm run dev`，可以在浏览器中查看到下面的截图效果，背景图已经被加载出来了--

 ![webpakc_intro](./assets/imgs/webpack_intro.jpg)