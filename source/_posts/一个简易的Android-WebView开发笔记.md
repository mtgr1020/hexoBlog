---
title: 一个简易的Android-WebView开发笔记
date: 2019-01-03 16:10:40
tags:
---

&nbsp;&nbsp;&nbsp;&nbsp;前段时间做了一个创新周的项目，需要在电视上展示，当时是用笔记本投屏，展会以后我就在想做一个安卓应用在电视上安装，省去投屏的烦恼，上午就找到了`少侠好剑法`同学进行技术上的指导，让我这个安卓小白也拥有了自己的应用，特此记录以供参考。

# 下载安卓开发工具

好剑少侠给我推荐的开发工具是[android studio](http://www.android-studio.org/index.php/download/hisversion)版本3.0，少侠说3.0以上的有问题
<img src="">

下载完毕以后就点击安装，我的是mac其他系统没有尝试，但是问题应该类似，首先会出来一个提示
<img src="http://pkhjrimz1.bkt.clouddn.com/WechatIMG30.png" width="50%" height="50%">
我的操作步骤是点击`Setup Proxy`,然后勾选第二个自动，在到这个页面点击Cancel,然后就会开始下载
<img src="http://pkhjrimz1.bkt.clouddn.com/WechatIMG37.png" width="70%" height="70%">
完成以后就会出来一个提示页，点击`Start a new Android Studio project`创建一个新的项目，在 select SDK的时候勾选第一个就OK了，进入主页面以后，看最下边的message中会有一些错误提示，点击
<img src="http://pkhjrimz1.bkt.clouddn.com/WechatIMG48.jpeg">
开始安装就可以了，都装好以后拿出来你的安卓手机，找到开发者选项，在开发者模式中把USB调试打开，点击下图中的绿色按钮
<img src="http://pkhjrimz1.bkt.clouddn.com/WX20190103-170032@2x.png" width="60%" height="60%">
如果不出意外的话，手机上就会出现一个hello world。

# C、V大法
## 布局界面
文件目录：***/app/src/main/res/layout/activity_main.xml
```
<?xml version="1.0" encoding="utf-8"?>

<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
android:layout_width="match_parent"
android:layout_height="match_parent"
android:orientation="vertical"
android:background="#F0FFF0" >

    <WebView
        android:id="@+id/web"
        android:layout_width="fill_parent"
        android:layout_height="fill_parent" />

</LinearLayout>
```

## Activity页面
文件目录： ***/app/src/main/java/com/example/～/～/MainActivity.java
```
public class MainActivity extends Activity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {

        super.onCreate(savedInstanceState);

        setContentView(R.layout.activity_main);
        WebView web=(WebView) findViewById(R.id.web);
        web.loadUrl("https://www.baidu.com/");

        web.getSettings().setJavaScriptEnabled(true);  //加上这一行网页为响应式的
        web.setWebViewClient(new WebViewClient(){
            @Override
            public boolean shouldOverrideUrlLoading(WebView view, String url) {
                view.loadUrl(url);
                return true;   //返回true， 立即跳转，返回false,打开网页有延时
            }
        });
    }

}
```
这个会遇到你粘贴过去都飘红，是因为有些包没有import，mac操作快捷键是option+enter，import以后就正常了。

## 添加网络权限
文件目录： ***/app/src/main/AndroidManifest.xml
```
<uses-permission android:name="android.permission.INTERNET" ></uses-permission>
<application    在此之前添加以上代码
```
搞定了～在点击运行即可在手机上看到webview。

# 打包APK

如有兴趣请[点击此处](https://jingyan.baidu.com/article/c843ea0bbfae3777931e4ac3.html),唯一不同的就是在最后一步把V1V2都勾上，别的按照那个网页来就行，少侠好剑法要求我这么点的，最后出一个提示
<img src="http://pkhjrimz1.bkt.clouddn.com/WechatIMG209.png">
最后apk地址在/***/app/release/ 下边，可以复制到安卓手机、电视端进行安装就可以了。
