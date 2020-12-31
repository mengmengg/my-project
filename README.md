# myproject

> A Vue.js project

## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build

# build for production and view the bundle analyzer report
npm run build --report
```

For a detailed explanation on how things work, check out the [guide](http://vuejs-templates.github.io/webpack/) and [docs for vue-loader](http://vuejs.github.io/vue-loader).
#### 搭建vue脚手架项目

```**tex
1.使用git
全局安装vue-cli
cnpm install --global vue-cli
2.创建一个基于webpack模板的新项目
vue init webpack my-project
3.安装依赖包
cd my-project
cnpm install
npm run dev运行项目
打包
npm run build
```

**打包中遇到的问题** 

```tex
1.页面空白(这是因为在打包的时候,没有修改路径,build默认打包路径是根路径,所以需要在修改的文件路径如下)
解决方案:
* 在config index.js文件中找到 build下的assetsPublicPath 修改成如下:
```

```js
 build: {
    // Template for index.html
    index: path.resolve(__dirname, '../dist/index.html'),

    // Paths
    assetsRoot: path.resolve(__dirname, '../dist'),
    assetsSubDirectory: 'static',
    assetsPublicPath: './',
 }
```

```js
* build文件下的utils.js文件下的 publicPath修改成如下:
// Extract CSS when that option is specified
    // (which is the case during production build)
    if (options.extract) {
      return ExtractTextPlugin.extract({
        use: loaders,
        fallback: 'vue-style-loader',
        publicPath:'../../'
      })
    } else {
      return ['vue-style-loader'].concat(loaders)
    }
  }
}
```

```js
* build文件下的webpack.prod.conf.js文件下的publicPath原先没有要加上
output: {
    path: config.build.assetsRoot,
    publicPath:'./',
    filename: utils.assetsPath('js/[name].[chunkhash].js'),
    chunkFilename: utils.assetsPath('js/[id].[chunkhash].js')
  },
```



##### 使用 jquery

vue中提供了dome，但是不支持。

vue是虚拟dom，在mounted下面都在真实dom，

使用vue+jquery的时候可以这样的写，但是得写在mounted（）挂载之后 下面

```js
1.npm install jquery 或cnpm install jquery
2.在main.js文件 import $ from 'jquery' （mian.js引入是全部文件都可以使用了，如果不需要全部文件使用可以只在使用的文件中引用）
3.使用
<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      a:false,
      outerVisible: false,
      innerVisible: false
    }

  },mounted(){//jquery 操作
    alert($("#ss").text())
  }
}
</script>
```



#####  axios



```js
1.npm install axios --save 或 cnpm install axios --save
使用方法1.在main文件写入
import axios from 'axios'
Vue.prototype.$axios = axios
其他文件
  created(){

    this.$axios.get('https://geo.datav.aliyun.com/areas/bound/geojson?code=100000').then(function(res){
      console.log(res)
    }).catch(function (error) {
      console.log(error);
    });
  },
}
使用方法2.
在使用的文件中引入
import axios from 'axios'
使用方法
  created(){
    axios.get('https://geo.datav.aliyun.com/areas/bound/geojson?code=100000').then(function(res){
      console.log(res)
    }).catch(function (error) {
      console.log(error);
    });
  },
}

```



##### element-ui

```js
cnpm install element-ui -D
cnpm install style-loader -D
npm install url-loader/cnpm install url-loader -D
在main.js中引入
import ElementUI from ‘element-ui’;
import ‘element-ui/lib/theme-chalk/index.css’;
//使用组件
Vue.use(ElementUI);
//在package.json中配置

 {
     test: /\.(woff|svg|eot|ttf)\??.*$/,
     loader: 'url-loader'
 },
 {
    test: /\.css$/,
     loader: 'style-loader!css-loader',
     exclude: /node_modules/
 }
```
