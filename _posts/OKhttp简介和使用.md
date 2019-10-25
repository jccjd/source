---
date: 2018-05-02
tags:
- Android

---

##   **简介**

android网络框架之OKhttp  
一个处理网络请求的开源项目,是安卓端最火热的轻量级框架,由移动支付Square公司贡献(该公司还贡献了Picasso)
用于替代HttpUrlConnection和Apache HttpClient
#### 官方资料
>[官方介绍](http://square.github.io/okhttp/)

>[github源码](https://github.com/square/okhttp)
#### 优势
 - 允许连接到同一个主机地址的所有请求,提高请求效率
 - 共享Socket,减少对服务器的请求次数  

- 通过连接池,减少了请求延迟
- 缓存响应数据来减少重复的网络请求  
- 减少了对数据流量的消耗
- 自动处理GZip压缩

#### 功能
- get,post请求
- 文件的上传下载
- 加载图片(内部会图片大小自动压缩)
- 支持请求回调，直接返回对象、对象集合
- 支持session的保持
>

####  效果图
![image](https://github.com/jccjd/L_OkHttp/blob/master/app/src/main/res/drawable/l1525091941778.gif?raw=true)

#### 相关使用
>添加依赖（build.gradle）

```
    compile 'com.squareup.okhttp3:okhttp:3.10.0'
```
>添加网络设置

```
    <uses-permission android:name="android.permission.INTERNET"/>
```


###### Get
1. 通过build来创建一个Request请求，可以不设置get默认方法就是get
url是访问地址（BASE_URL这里用的是虚拟机的基地址）

```
String BASE_URL = "http://10.0.2.2/get.php?key=get";
        OkHttpClient okHttpClient = new OkHttpClient();

        Request request = new Request.Builder()
        .url(BASE_URL)
        .get()
        .build();
```


2. 创建Call对象参数就是Request请求对象发送请求

```
        Call call = okHttpClient.newCall(request);
        call.enqueue(callback);

```
3.然后以异步方式执行请求

```
 okHttpUtil.requestGet(new Callback() {
            //请求失败执行方法
            @Override
            public void onFailure(Call call, IOException e) {}

            //请求成功执行方法，request就是从服务器得到参数，request.body()可以得到任意类型，字符串，字节。
            @Override
            public void onResponse(Call call, Response response) throws IOException {
                String strRet = response.body().string();
                //将数据存到Handler中
                Message msg = mHandler.obtainMessage();
                msg.obj = "Get方法获取数据 ----> "+"  " + strRet;
                mHandler.sendMessage(msg);
            }
        });
    }
```
###### Post
Post与get类似 post的参数是包含在请去体中所以需要Formbody添加键值对

```
        FormBody formBody = new FormBody.Builder().add("key", "Post").build();
```
其他部分大致相同

```
public static void requestPost(Callback callback) {
        String BASE_URL = "http://10.0.2.2/post.php";
        OkHttpClient okHttpClient = new OkHttpClient();
        FormBody formBody = new FormBody
                .Builder()
                .add("key", "Post")
                .build();

        Request request = new Request
                .Builder()
                .url(BASE_URL)
                .post(formBody)
                .build();

        Call call = okHttpClient.newCall(request);
        call.enqueue(callback);
    }

     private void httpPost() {
        okHttpUtil.requestGet(new Callback() {
            @Override
            public void onFailure(Call call, IOException e) {

            }

            @Override
            public void onResponse(Call call, Response response) throws IOException {
                String strRet = response.body().string();
                Message msg = mHandler.obtainMessage();
                msg.obj = "Post方法获取数据 ---> "+"  " +strRet;
                mHandler.sendMessage(msg);

            }
        });
    }
```
源码见我的github --> [jccjd](https://github.com/jccjd/L_OkHttp/)
