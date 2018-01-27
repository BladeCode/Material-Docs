# jQueryMobile常用技巧
2016-01-09 20:19:00

jQueryMobile是基于html5的用户界面系统设计,使响应web站点和应用程序都可以访问所有的智能手机,平板电脑和桌面设备。  
在使用jQueryMobile框架来构建WebApp过程中，或多或少都会遇到一些问题，下面总结常遇问题的解决方法

## CSS样式
1. 样式不能正常加载
    * 问题描述：引用好jQuery，jQueryMobile库，不加载样式
    * 解决方法：需要先引用jQuery库，再引用jQueryMobile库
    * 原理：jQueryMobile库是在jQueryMobile库上的延展，所以必须先引用先引用jQuery库，再引用jQueryMobile库
2. 页面不能正常缩放
    * 问题描述：在不同分辨率下，页面不能响应式根据屏幕大小正常显示
    * 解决方法：需要在<head>标签中加入  
    ``` html
    "<meta name = "viewport" content = "width=device-width, initial-scale=1">"
    ```
    * 原理：width属性控制视口的宽度。`#!js initial-scale `属性控制页面最初加载时的缩放等级。`#!js maximum-scale `、`#!js minimum-scale `及`#!js user-scalable `属性控制允许用户以怎样的方式放大或缩小页面（可省略）。
    
    !!! Info
        [具体见火狐开发者文档详细介绍](https://developer.mozilla.org/zh-CN/docs/Mobile/Viewport_meta_tag)

3. 页面之间跳转，样式丢失
    * 问题描述：当从A页面跳转到B页面（根据传入的数据动态加载），会造成B页面动态生成的样式丢失
    * 解决方法：
        * 将页面引入的标准css和js写入到
        ``` html 
        <div data-role="page"> 
        ```
        * 通过禁止默认使用Ajax进行跳转
            1. 局部禁止：在a标签中加入`#!js data-ajax="false" `属性  
            当需要正常的http请求而不用Ajax请求，比如链接到别的网站等情况。在a标签中加入`#!js rel=external `属性
            2. 全局禁止： ==js== 代码如下（该代码片段需要放在`jquery.mobile-xxx.min.js`引入之前）
            ```javascript
            $(document).bind("mobileinit",function(){
                // disable ajax nav
                $.mobile.ajaxEnabled=false
            });
            ```
    * 原理：在jQuery Mobile中，页面跳转默认是使用ajax进行。这样就会只将B页面`#!html <div data-role="page">`内的内容加载进DOM，而之外引用的标准样式就不会加载进来，从而造成B页面中css和js都将失效
4. Jqm默认样式边缘，focus事件阴影
    * 问题描述：触摸点击聚焦边缘出现阴影
    * 解决方法：删除`jquery.mobile-xxx.min.css`文件第1053行这段代码
5. Jqm跳转“闪屏”
    * 问题描述：在使用jQueryMobile页面之间的跳转，会出现每跳转一次，屏幕就会出现一次白屏
    * 解决方法：
        * [官方给出解释](http://demos.jquerymobile.com/1.2.0/docs/pages/page-transitions.html)在引用css中加入如下代码：
        ```css
        .ui-page { -webkit-backface-visibility: hidden; }
        ```
        然而并没有什么用  
        * 其他方法，首先可以设置闪屏的背景颜色和原背景颜色一样
        ```css
        .ui-overlay-a {
            border: 1px solid #AAA;
            color: #333;
            background: #F9F9F9;
        }
        ```
        其次，在跳转的a标签中加入禁用ajax默认跳转方式`#!js data-ajax="false"`，和`#!js data-prefetch`属性
6. 触发按钮等控件，事件响应迟缓
    * 问题描述：当点击按钮，或者滑动屏幕，发现事件响应有些迟缓
    * 解决方法：
    ``` javascript
    $.mobile.buttonMarkup.hoverDelay = "false"
    ```
7. 自定义页面， ==header== ， ==footer== 出现跳动
    * 问题描述：自定义页面，当内容超过当前屏幕垂直方向高度，点击屏幕中间，出现， ==footer== 跳动
    * 解决方法：在 ==header== ， ==footer== 标签中加入
    ``` javascript
    data-tap-toggle="false"
    ```
8. 去除jQueryMobile默认样式
    * 问题描述：有时在开发过程中，我们需要自定义某个组件的样式，不需要自带的默认样式
    * 解决方法：在该组件标签中加入
    ``` javascript
    data-role='none'
    ```
    * 其他补充：当不需要默认的按钮阴影和圆角效果，在按钮标签中加入`#!js data-shadow="false"`取消阴影,`#!js data-corners="false"`取消圆角