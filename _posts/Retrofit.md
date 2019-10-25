---
date: 2018-05-14
tags:
- Android
---
##### Json是什么？
json(Javascript Object Notation)是一种轻量级的数据交换格式，相比于xml这种数据交换格式来说，
因为解析xml比较的复杂，而且需要编写大段的代码，所以客户端和服务器的数据交换格式往往通过json来进行交换。
尤其是对于web开发来说，json数据格式在客户端直接可以通过javascript来进行解析。

![image](http://www.json.org/object.gif)

json一共有两种数据结构，一种是以 (key/value)对形式存在的无序的jsonObject对象，
一个对象以“{”（左花括号）开始，“}”（右花括号）结束。每个“名称”后跟一个“:”（冒号）；
“‘名称/值’ 对”之间使用“,”（逗号）分隔。

![image](http://www.json.org/array.gif)

例如：{"name": "xiaoluo"}， 这就是一个最简单的json对象，对于这种数据格式，key值必须要是string类型，
而对于value，则可以是string、number、object、array等数据类型：

![image](http://www.json.org/value.gif)

关于详尽数据格式参见 --> [http://www.json.org/json-zh.html](https://note.youdao.com/)

##### 概述
本文主要阐述的有关于用retrofit来获取服务器端json数据, 并进行解析，相关demo在(https://github.com/jccjd/L_json)上

---

Retrofit是一套RESTful架构的Android(Java)客户端实现，基于注解，提供JSON to POJO(Plain Ordinary Java Object,简单Java对象)，POJO to JSON，网络请求(POST，GET,PUT，DELETE等)封装

**类结构如图**

![image](https://github.com/jccjd/L_json/blob/master/app/src/main/res/drawable/buhuo.PNG?raw=true)

先添加依赖

```
    compile 'com.squareup.retrofit2:retrofit:2.4.0'
    compile 'com.squareup.retrofit2:converter-gson:2.4.0'
```

需要解析的json字符是这样的

```
<?php
 for ($i=0; $i < 5 ; $i++) {
 	# code...
 	$newsArray[$i] = array('title'=>'biaoti'.$i,'content'=>'neirong','newsImageUrl'=>'http//10.0.2.2/image/news/1.jpg');
 }
 $jsonArray = array('code'=>0,'message'=>'success','data'=>$newsArray);
 echo json_encode($jsonArray);
```
httpResult通过定义泛型

利用接口和注解创建ApiService

```
public interface ApiService {

    @GET("json.php")

    Call<HttpResult<List<news>>> getNews();
}
```


然后是简单的布局就一个button绑定事件 和 一个TextView显示获取的数据

```
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout
        xmlns:android="http://schemas.android.com/apk/res/android"
        xmlns:tools="http://schemas.android.com/tools"
        xmlns:app="http://schemas.android.com/apk/res-auto"
        android:layout_width="match_parent"
        android:orientation="vertical"
        android:layout_height="match_parent"
        tools:context="com.example.lenovo.l_json.MainActivity">

    <Button android:layout_width="wrap_content" android:layout_height="wrap_content"
    android:id="@+id/btn_Json"/>

    <TextView
            android:layout_width="wrap_content"
            android:id="@+id/tv_show_msg"
            android:layout_height="wrap_content"
            android:text="Hello World!"
            app:layout_constraintBottom_toBottomOf="parent"
            app:layout_constraintLeft_toLeftOf="parent"
            app:layout_constraintRight_toRightOf="parent"
            app:layout_constraintTop_toTopOf="parent"/>

</LinearLayout>
```
