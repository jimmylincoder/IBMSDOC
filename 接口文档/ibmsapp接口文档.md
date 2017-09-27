<link rel="stylesheet" href="http://yandex.st/highlightjs/6.2/styles/googlecode.min.css">
 
<script src="http://code.jquery.com/jquery-1.7.2.min.js"></script>
<script src="http://yandex.st/highlightjs/6.2/highlight.min.js"></script>
 
<script>hljs.initHighlightingOnLoad();</script>
<script type="text/javascript">
 $(document).ready(function(){
      $("h2,h3,h4,h5,h6").each(function(i,item){
        var tag = $(item).get(0).localName;
        $(item).attr("id","wow"+i);
        $("#category").append('<a class="new'+tag+'" href="#wow'+i+'">'+$(this).text()+'</a></br>');
        $(".newh2").css("margin-left",0);
        $(".newh3").css("margin-left",20);
        $(".newh4").css("margin-left",40);
        $(".newh5").css("margin-left",60);
        $(".newh6").css("margin-left",80);
      });
 });
</script>
<div id="category"></div>
#IBMSApp接口文档

##一、文档范围

本文主要描述IBMSApp接口规范和接口列表。

##二、接口规范

###（1）请求

使用标准的HTTP POST请求，请求参数为JSON（UTF-8）格式。

请求地址为:http://ip:port/api

```
{
	 //应用包名
     "app_name":"com.suntek.ibmsapp",
     
     //应用版本
     "app_version":"1.0",
     
     //操作系统
     "os":"Android",
     
     //操作系统版本
     "os_version":"6.0.1",
     
     //请求参数
     "params":
     {
     	"key" : "value"
     },
     
     //服务名
     "service":"model.action",
     
     //uuid
     "udid":"864454032160446"
}

```

###(2)应答

使用JSON（UTF-8）返回数据,以下为应答格式

```
{
	//状态码
	"code":200,
	
	//返回数据
	"data":{}
	
	//提示消息
	"message": ""
}

```

## 三、数据类型

###(1)用户- User

```
{
	// 用户code -- String
	"user_code" : "admin",
	
	//用户名 -- String
	"user_name" : “系统管理员”,
	
	//密码 -- String
	"password" : “suntek”,
}

```

###(2)摄像机- Camera

```
{
    //id -- String
    "id": "454",

	//通道号 -- String
    "channel": "33",
    
    //nvr ip -- String
    "ip": "172.16.16.111",
    
    //摄像机名称 -- String
    "name": "停车场_通道33",
    
    //所属区域代码 -- String
    "org_code": "010Q",
    
    //nvr密码 -- String
    "password": "suntek",
    
    //所在区域名称 -- String
    "place": "停车场",
    
    //nvr 端口 -- String
    "port": "8000",
    
    //摄像机类型 -- String
    "type": "1",
    
    //nvr 用户名 -- String
    "user_name": "admin"

}

```

###(3)区域- Area

```
{
	//id  -- String
    "id": "67",
   
   	//区域名称  -- String
    "name": "一栋",
   	
   	//区域级别  -- String
    "node_level": "2",
   
   	//区域代码  -- String
    "org_code": "010K",
   
    //父节点代码  -- String
    "parent_id": "1"
}

```

###(4)录像- RecordItem

```
{
	//id  -- String
    "device_id": "44394293492384",
   
   	//开始时间  -- String
    "start_time": "2017-07-27T09:18:14",
   	
   	//结束时间  -- String
    "end_time": "2017-07-27T10:28:44"
}

```

## 四、接口列表

###(一)用户

#### 1. 登录：user.login
> 请求参数

| 参数名 | 类型 | 是否必须 | 说明 | 示例 |
| --- |:---:| ---:| -----:| -----:|
| user_name | String | Y | 用户名 | "admin" |
| password | String | Y | 密码 | "suntek"|

> 应答结果

| key | value类型 | 说明 | 示例 |
| --- |:---:| ---:| -----:| -----:|
| user| User| 用户实体 | 参`数据类型 - 用户`| 

###(二)摄像机
#### 1. 摄像机列表：camera.list
> 请求参数

| 参数名 | 类型 | 是否必须 | 说明 | 示例 |
| --- |:---:| ---:| -----:| -----:|
| area_id | String | Y | 区域id | "01" |
| page | String | Y | 页数 | "1"|

> 应答结果

| key | value类型 | 说明 | 示例 |
| --- |:---:| ---:| -----:| -----:|
| camera_list| List&lt;Camera&gt;| 摄像机列表 | 参`数据类型 - 摄像机`| 
| total_page| int| 总页数 | `1`| 

#### 2. 添加历史播放：camera.add_history
> 请求参数

| 参数名 | 类型 | 是否必须 | 说明 | 示例 |
| --- |:---:| ---:| -----:| -----:|
| camera_id | String | Y | 摄像机id | "100" |

> 应答结果

无

#### 3. 历史播放列表：camera.history_list
> 请求参数

| 参数名 | 类型 | 是否必须 | 说明 | 示例 |
| --- |:---:| ---:| -----:| -----:|
| page | String | Y | 页数 | "1"|

> 应答结果

| key | value类型 | 说明 | 示例 |
| --- |:---:| ---:| -----:| -----:|
| camera_list| List&lt;Camera&gt;| 摄像机列表 | 参`数据类型 - 摄像机`| 
| total_page| int| 总页数 | `1`| 

#### 4. 摄像机搜索：camera.list_by_keyword
> 请求参数

| 参数名 | 类型 | 是否必须 | 说明 | 示例 |
| --- |:---:| ---:| -----:| -----:|
| page | String | Y | 页数 | "1"|
| keyword | String | Y | 关键字 | "通道"|


> 应答结果

| key | value类型 | 说明 | 示例 |
| --- |:---:| ---:| -----:| -----:|
| camera_list| List&lt;Camera&gt;| 摄像机列表 | 参`数据类型 - 摄像机`| 
| total_page| int| 总页数 | `1`| 

###(三)区域
#### 1. 区域列表：area.list

> 请求参数

| 参数名 | 类型 | 是否必须 | 说明 | 示例 |
| --- |:---:| ---:| -----:| -----:|
| parent_id | String | Y | 父id | "01"|


> 应答结果

| key | value类型 | 说明 | 示例 |
| --- |:---:| ---:| -----:| -----:|
| area_list| List&lt;Area&gt;| 区域列表 | 参`数据类型 - 区域`| 

###(四)视频播放控制

#### 1. 播放实时或历史：camera.play
> 请求参数

| 参数名 | 类型 | 是否必须 | 说明 | 示例 |
| --- |:---:| ---:| -----:| -----:|
| device_id | String | Y | 设备编码 | "40023402342342"|
| device_ip | String | Y | nvr ip | "172.16.16.111"|
| channel | String | Y | 通道号 | "33"|
| user | String | Y | nvr用户名 | "admin"|
| password | String | Y | nvr密码 | "suntek"|
| begin_time | String | N | 录像开始时间 | ""|
| end_time | String | YN | 录像结束时间 | ""|


> 应答结果

| key | value类型 | 说明 | 示例 |
| --- |:---:| ---:| -----:| -----:|
| address| String| 视频播放地址 | `rtmp://live.hkstv.hk.lxdns.com/live/hks`| 
| session| String| session | `34oi34uo3iu4`| 

#### 2. 停止实时或历史：camera.stop
> 请求参数

| 参数名 | 类型 | 是否必须 | 说明 | 示例 |
| --- |:---:| ---:| -----:| -----:|
| session | String | Y | 视频播放session | "safjoweirw"|

> 应答结果

无

#### 3. 暂停历史播放：camera.pause
> 请求参数

| 参数名 | 类型 | 是否必须 | 说明 | 示例 |
| --- |:---:| ---:| -----:| -----:|
| session | String | Y | 视频播放session | "safjoweirw"|

> 应答结果

无


#### 4. 恢复播放：camera.resume
> 请求参数

| 参数名 | 类型 | 是否必须 | 说明 | 示例 |
| --- |:---:| ---:| -----:| -----:|
| session | String | Y | 视频播放session | "safjoweirw"|

> 应答结果

无


#### 5. 改变速度：camera.change_speed
> 请求参数

| 参数名 | 类型 | 是否必须 | 说明 | 示例 |
| --- |:---:| ---:| -----:| -----:|
| session | String | Y | 视频播放session | "safjoweirw"|
| speed | String | Y | 播放速度 | "2.0"|


> 应答结果

无

#### 6. 改变位置：camera.change_position
> 请求参数

| 参数名 | 类型 | 是否必须 | 说明 | 示例 |
| --- |:---:| ---:| -----:| -----:|
| session | String | Y | 视频播放session | "safjoweirw"|

> 应答结果

无

#### 7. 查询录像：camera.query

> 请求参数

| 参数名 | 类型 | 是否必须 | 说明 | 示例 |
| --- |:---:| ---:| -----:| -----:|
| device_id | String | Y | 设备编码 | "40023402342342"|
| device_ip | String | Y | nvr ip | "172.16.16.111"|
| channel | String | Y | 通道号 | "33"|
| user | String | Y | nvr用户名 | "admin"|
| password | String | Y | nvr密码 | "suntek"|
| begin_time | String | Y | 录像开始时间 | ""|
| end_time | String | Y | 录像结束时间 | ""|


> 应答结果

| key | value类型 | 说明 | 示例 |
| --- |:---:| ---:| -----:| -----:|
| records |  List&lt;RecordItem&gt;| 历史视频列表 | 参`数据类型 - 录像`| 
















