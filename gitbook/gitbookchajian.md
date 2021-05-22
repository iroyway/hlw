# gitbook插件
## 自己常用的gitbook插件
### 代码复制
```
"code"
```
### 文件和目录自己调整
```
"splitter"
```
### 隐藏不必要的链接
```
"hide-element"
```
### 目录悬浮             
```
"page-toc-button"
```
### 回到顶部 
```
"back-to-top-button"
```
### 导航目录折叠
```
"chapter-fold"
```
### 页面底部添加信息
```
"tbfed-pagefooter"
```

### prism插件 
系统自带插件的高亮功能并不完善，可使用prism插件增强，该插件需要先禁用highlight插件```
```
"-highlight",
"prism"
```
如果需要修改背景色、字体大小等，可以在 website.css 定义 pre[class*="language-"] 类来修改，下面是一个示例：
```
pre[class*="language-"]{
    border: none;
    background-color:#f7f7f7;
    font-size:1em;
    line-height:1.2em;
}
```
## 插件安装
```
gitbook install
```

## 整个代码如下：
```
{
    "title": "我的互联网之路学习笔记",
    "author": "iroyway",
    "links" : {
        "sidebar" : {
            "Home" : "https://iroyway.github.io/hlw/"
        }
    },
    "plugins": [
        "-lunr", 
        "-search", 
        "-highlight",
        "prism",
        "code", 
        "search-pro",
        "splitter",
        "-chapter-fold",
        "hide-element",
        "page-toc-button",
        "back-to-top-button",
        "tbfed-pagefooter"
    ],
    "pluginsConfig": {
        "hide-element": {
            "elements": [
                ".gitbook-link"
            ]
        },
        "page-toc-button": {
            "maxTocDepth": 2,
            "minTocSize": 2
        },
        "tbfed-pagefooter": {
            "copyright": "Copyright &copy iroyway 2019 all right reserved.powered by Gitbook",
            "modify_label": "该文章修订时间：",
            "modify_format": "YYYY-MM-DD HH:mm:ss"
        },
        "prism": {
            "css": [
              "prismjs/themes/prism-solarizedlight.css"
            ]
        },
        "theme-default": {
            "showLevel": true
        }
    }
}
```