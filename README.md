# VoiceShare
一个轻量级的社交平台服务端
# 简介
【声享】基于 SSH 框架进行开发，遵循 MVC 模式并采用三层架构。数据库采用 MySQL。  
可满足社交平台常用功能，如：浏览广场，浏览关注的人发表的动态，对动态进行点赞评论等交互，接收通知提醒，用户个人管理和设置等功能。
# 特性
- 可按时间、地点、热度、智能推荐等方式浏览动态广场。
- 基于协同过滤算法，实现非集群服务器环境下实时计算返回用户协同数据，该算法应用于“为你推荐”功能。
- 通过时间戳请求方式，节省请求流量。
- 优化数据表结构和查询语句，减轻服务器接收请求处理压力。
- 多次机制严格校验，防止请求攻击和破坏数据安全。
- 编码规范，易于阅读和扩展。  

# 使用
下载项目，创建数据库，修改项目中`jdbc.properties`数据库配置文件，启动Tomcat，一切就绪。  

# <center>VoiceShare API </center>
---
## <span id = "backToTop">用户</span>
|读取接口|描述|
|:-------------|:-------------|
| [user/verify_phone_num](#user/verify_phone_num) | 手机号是否已存在 |
| [user/verify_user_name](#user/verify_user_name) | 用户名是否已存在 |
| [user/user_info](#user/user_info) | 获取用户信息 |
| [user/search_users](#user/search_users) | 查找用户 |
| [user/upload_token](#user/upload_token) | 获取上传凭证|
| [user/friends](#user/friends) | 获取某用户关注的用户列表|
| [user/followers](#user/followers) | 获取某用户关注的关注者|
| [user/unread_count](#user/unread_count) | 获取某用户的未读消息数|

|写入接口|描述|
|:-------------|:-------------|
| [user/register](#user/register) | 注册 |
| [user/login](#user/login) |  登录 |
| [user/follow](#user/follow) | 关注某用户 |
| [user/cancle_follow](#user/cancle_follow) | 取消关注某用户 |
| [user/modify_personal_info](#user/modify_personal_info) | 修改个人信息 |

---
## 动态
|读取接口|描述|
|:-------------|:-------------|
| [dynamic/timeline](#dynamic/timeline) | 获取公共默认动态（按时间） |
| [dynamic/hot](#dynamic/hot) | 获取公共热门动态 |
| [dynamic/nearby](#dynamic/nearby) | 获取公共附近动态 |
| [dynamic/recommend](#dynamic/recommend) | 获取推荐的公共动态 |
| [dynamic/friends](#dynamic/friends) | 得到关注的人的动态 |
| [dynamic/history](#dynamic/history) | 获取某用户发表过的所有动态 |

|写入接口|描述|
|:-------------|:-------------|
| [users/dynamic/listen](#dynamic/listen) | 听一条动态 |
| [users/dynamic/publish](#dynamic/publish) | 发表一条动态 |
| [users/dynamic/delete](#dynamic/ldelete) | 删除一条动态 |


---
## 评论
|读取接口|描述|
|:-------------|:-------------|
| [comment/comments](#comment/comments) | 获得某一条动态的评论 |
| [comment/to_me](#comment/to_me) | 我收到的评论 |

|写入接口|描述|
|:-------------|:-------------|
| [comment/create](#comment/create) | 评论一条动态（点赞也算评论） |
| [comment/delete](#comment/delete) | 删除一条评论 |

---
.
 
. 
 
# 接口详情
---

## <span id = "user/verify_phone_num">user/verify_phone_num</span>[回到顶部](#backToTop)
---
手机号是否已存在  

## 支持格式

---

JSON
## HTTP请求方式

---

GET
## 请求参数
---
| | 必选 | 类型 | 说明 |
|:-------------|:-------------|:-------------|
| phoneNum | true | string | 手机号 |

## 调用样例

---

```
user/verify_phone_num?phoneNum=18612345678
```

## 成功返回结果

---

*** JSON示例 ***

```

{
status: 1
}

```


关于其它错误返回值与错误代码，参见 [错误代码说明](#errorcode)
## 返回字段说明
---
|返回值字段 | 字段类型 | 字段说明 |
|:-------------|:-------------|:-------------|
| status |  string | 状态，成功为 1 |
  
.
 
. 

## <span id = "user/verify_user_name">user/verify_user_name</span> [回到顶部](#backToTop)
---
用户名是否已存在  

## 支持格式

---

JSON
## HTTP请求方式

---

GET
## 请求参数
---
| | 必选 | 类型 | 说明 |
|:-------------|:-------------|:-------------|
| userName | true | string | 用户名 |

## 调用样例

---

```
user/verify_user_name?userName=张三
```

## 成功返回结果

---

*** JSON示例 ***

```

{
status: 1
}

```


关于其它错误返回值与错误代码，参见 [错误代码说明](#errorcode)
## 返回字段说明
---
|返回值字段 | 字段类型 | 字段说明 |
|:-------------|:-------------|:-------------|
| status |  string | 状态，成功为 1 |
  
.
 
. 

## <span id = "user/user_info">user/user_info</span> [回到顶部](#backToTop)
---
获取用户信息 

## 支持格式

---

JSON
## HTTP请求方式

---

GET
## 请求参数
---
| | 必选 | 类型 | 说明 |
|:-------------|:-------------|:-------------|
| accessToken | true | string | 用户凭证 |
| searchUserId | true | string | 要查询的用户id |

## 调用样例

---

```
user/user_info?accessToken=cb57ca2ad7722fd8ec39c0327f7c8801&searchUserId=1
```

## 成功返回结果

---

*** JSON示例 ***

```

{
user: {
avatar: "http://www.baidu.com",
createTime: 1462716192421,
description: "哈哈",
dynamicCount: 7,
followersCount: 20,
friendsCount: 30,
id: 1,
lantitude: 40.5,
longtitude: 120.2,
phoneNum: "15659173545",
unreadCount: 5,
userName: "rush"
},
alreadyFollowed: true
}

```


关于其它错误返回值与错误代码，参见 [错误代码说明](#errorcode)
## 返回字段说明
---
|返回值字段 | 字段类型 | 字段说明 |
|:-------------|:-------------|:-------------|
| avatar |  string | 头像图片地址 |
| createTime |  int64 | 用户注册时间 |
| description |  string | 用户个性签名 |
| dynamicCount |  int | 用户发表过的动态数 |
| followersCount |  int | 用户关注者数量 |
| friendsCount |  int | 用户关注的人的数量 |
| id |  int64 | 用户id |
| lantitude |  string | 用户地理位置纬度 |
| longtitude |  string | 用户地理位置经度 |
| phoneNum |  string | 用户手机号 |
| unreadCount |  int | 用户消息未读数 |
| userName |  string | 用户名 |
| alreadyFollowed |  boolean |  当前用户是否已经关注了该查询用户 |

.
 
. 

## <span id = "user/search_users">user/search_users</span> [回到顶部](#backToTop)
---
查找用户 

## 支持格式

---

JSON
## HTTP请求方式

---

GET
## 请求参数
---
| | 必选 | 类型 | 说明 |
|:-------------|:-------------|:-------------|
| accessToken | true | string | 用户凭证 |
| searchKeyword | true | string | 搜索关键字 |

## 调用样例

---

```
user/search_users?accessToken=cb57ca2ad7722fd8ec39c0327f7c8801&searchKeyword=张三
```

## 成功返回结果

---

*** JSON示例 ***

```

[
{
users: [
{
avatar: "http://www.baidu.com",
createTime: 1462716192421,
description: "哈哈",
dynamicCount: 7,
followersCount: 20,
friendsCount: 30,
id: 1,
lantitude: 40.5,
longtitude: 120.2,
phoneNum: "15659173545",
unreadCount: 5,
userName: "rush"
}
]
}
```


关于其它错误返回值与错误代码，参见 [错误代码说明](#errorcode)
## 返回字段说明
---
|返回值字段 | 字段类型 | 字段说明 |
|:-------------|:-------------|:-------------|
| avatar |  string | 头像图片地址 |
| createTime |  int64 | 用户注册时间 |
| description |  string | 用户个性签名 |
| dynamicCount |  int | 用户发表过的动态数 |
| followersCount |  int | 用户关注者数量 |
| friendsCount |  int | 用户关注的人的数量 |
| id |  int64 | 用户id |
| lantitude |  string | 用户地理位置纬度 |
| longtitude |  string | 用户地理位置经度 |
| phoneNum |  string | 用户手机号 |
| unreadCount |  int | 用户消息未读数 |
| userName |  string | 用户名 |

.
 
. 

## <span id = "user/upload_token">user/upload_token</span> [回到顶部](#backToTop)
---
获取上传凭证 

## 支持格式

---

JSON
## HTTP请求方式

---

GET
## 请求参数
---
| | 必选 | 类型 | 说明 |
|:-------------|:-------------|:-------------|
| accessToken | true | string | 用户凭证 |

## 调用样例

---

```
user/upload_token?accessToken=cb57ca2ad7722fd8ec39c0327f7c8801
```

## 成功返回结果

---

*** JSON示例 ***

```

{
uploadToken: "EMfZk8Ygx-VdL6SyjEggabaJAPE3uIcLpUVvO2j1:n5JoQqvfT5rUV2j-NPdxzgW8S3g=:eyJzY29wZSI6InJ1c2giLCJkZWFkbGluZSI6MTQ2MzU3Nzc5MH0="
}

```


关于其它错误返回值与错误代码，参见 [错误代码说明](#errorcode)
## 返回字段说明
---
|返回值字段 | 字段类型 | 字段说明 |
|:-------------|:-------------|:-------------|
| uploadToken |  string | 上传文件凭证 |


.
 
. 

## <span id = "user/friends">user/friends</span> [回到顶部](#backToTop)
---
获取某用户关注的用户列表

## 支持格式

---

JSON
## HTTP请求方式

---

GET
## 请求参数
---
| | 必选 | 类型 | 说明 |
|:-------------|:-------------|:-------------|
| accessToken | true | string | 用户凭证 |
| searchUserId | true | int64 | 要查询的用户id |
| sinceId | false | int64 | 若指定此参数，则返回id比sinceId大的动态（即比sinceId时间晚的微博），默认为0。 |
| maxId | false | int64 | 若指定此参数，则返回id比maxId小的动态（不能同时制定sinceId和maxId,否则不返回结果） |

## 调用样例

---

```
user/friends?accessToken=cb57ca2ad7722fd8ec39c0327f7c8801&searchUserId=1
```

## 成功返回结果

---

*** JSON示例 ***

```

{
users: [
{
avatar: "http://www.baidu.com",
createTime: 1462716192421,
description: "哈哈",
dynamicCount: 7,
followersCount: 20,
friendsCount: 30,
id: 1,
lantitude: 40.5,
longtitude: 120.2,
phoneNum: "15659173545",
unreadCount: 5,
userName: "rush"
}
]
}

```


关于其它错误返回值与错误代码，参见 [错误代码说明](#errorcode)
## 返回字段说明
---
|返回值字段 | 字段类型 | 字段说明 |
|:-------------|:-------------|:-------------|
| avatar |  string | 头像图片地址 |
| createTime |  int64 | 用户注册时间 |
| description |  string | 用户个性签名 |
| dynamicCount |  int | 用户发表过的动态数 |
| followersCount |  int | 用户关注者数量 |
| friendsCount |  int | 用户关注的人的数量 |
| id |  int64 | 用户id |
| lantitude |  string | 用户地理位置纬度 |
| longtitude |  string | 用户地理位置经度 |
| phoneNum |  string | 用户手机号 |
| unreadCount |  int | 用户消息未读数 |
| userName |  string | 用户名 |


.
 
. 

## <span id = "user/followers">user/followers</span> [回到顶部](#backToTop)
---
获取某用户的关注者

## 支持格式

---

JSON
## HTTP请求方式

---

GET
## 请求参数
---
| | 必选 | 类型 | 说明 |
|:-------------|:-------------|:-------------|
| accessToken | true | string | 用户凭证 |
| searchUserId | true | int64 | 要查询的用户id |
| sinceId | false | int64 | 若指定此参数，则返回id比sinceId大的微博（即比sinceId时间晚的微博），默认为0。 |
| maxId | false | int64 | 若指定此参数，则返回id比maxId小的微博（不能同时制定sinceId和maxId,否则不返回结果） |

## 调用样例

---

```
user/followers?accessToken=cb57ca2ad7722fd8ec39c0327f7c8801&searchUserId=1
```

## 成功返回结果

---

*** JSON示例 ***

```

{
users: [
{
avatar: "http://www.baidu.com",
createTime: 1462716192421,
description: "哈哈",
dynamicCount: 7,
followersCount: 20,
friendsCount: 30,
id: 1,
lantitude: 40.5,
longtitude: 120.2,
phoneNum: "15659173545",
unreadCount: 5,
userName: "rush"
}
]
}

```


关于其它错误返回值与错误代码，参见 [错误代码说明](#errorcode)
## 返回字段说明
---
|返回值字段 | 字段类型 | 字段说明 |
|:-------------|:-------------|:-------------|
| avatar |  string | 头像图片地址 |
| createTime |  int64 | 用户注册时间 |
| description |  string | 用户个性签名 |
| dynamicCount |  int | 用户发表过的动态数 |
| followersCount |  int | 用户关注者数量 |
| friendsCount |  int | 用户关注的人的数量 |
| id |  int64 | 用户id |
| lantitude |  string | 用户地理位置纬度 |
| longtitude |  string | 用户地理位置经度 |
| phoneNum |  string | 用户手机号 |
| unreadCount |  int | 用户消息未读数 |
| userName |  string | 用户名 |




.
 
. 

## <span id = "user/unread_count">user/unread_count</span> [回到顶部](#backToTop)
---
获取某用户的消息未读数

## 支持格式

---

JSON
## HTTP请求方式

---

GET
## 请求参数
---
| | 必选 | 类型 | 说明 |
|:-------------|:-------------|:-------------|
| accessToken | true | string | 用户凭证 |

## 调用样例

---

```
user/unread_count?accessToken=cb57ca2ad7722fd8ec39c0327f7c8801
```

## 成功返回结果

---

*** JSON示例 ***

```

{
unread_count: 5
}

```


关于其它错误返回值与错误代码，参见 [错误代码说明](#errorcode)
## 返回字段说明
---
|返回值字段 | 字段类型 | 字段说明 |
|:-------------|:-------------|:-------------|
| avatar |  string | 头像图片地址 |
| createTime |  int64 | 用户注册时间 |
| description |  string | 用户个性签名 |
| dynamicCount |  int | 用户发表过的动态数 |
| followersCount |  int | 用户关注者数量 |
| friendsCount |  int | 用户关注的人的数量 |
| id |  int64 | 用户id |
| lantitude |  string | 用户地理位置纬度 |
| longtitude |  string | 用户地理位置经度 |
| phoneNum |  string | 用户手机号 |
| unreadCount |  int | 用户消息未读数 |
| userName |  string | 用户名 |


.
 
. 

## <span id = "user/register">user/register</span> [回到顶部](#backToTop)
---
注册

## 支持格式

---

JSON
## HTTP请求方式

---

POST
## 请求参数
---
| | 必选 | 类型 | 说明 |
|:-------------|:-------------|:-------------|
| phoneNum | true | string | 手机号 |
| userName | true | string | 用户名 |
| smsCode | true | string | 短信验证码 |

## 调用样例

---

```
user/register?phoneNum=18012345678&userName=张三&smsCode=1234
```

## 成功返回结果

---

*** JSON示例 ***

```

{
status: 1
}

```


关于其它错误返回值与错误代码，参见 [错误代码说明](#errorcode)
## 返回字段说明
---
|返回值字段 | 字段类型 | 字段说明 |
|:-------------|:-------------|:-------------|
| status |  string | 状态，成功为 1 |



.
 
. 

## <span id = "user/login">user/login</span> [回到顶部](#backToTop)
---
登录

## 支持格式

---

JSON
## HTTP请求方式

---

POST
## 请求参数
---
| | 必选 | 类型 | 说明 |
|:-------------|:-------------|:-------------|
| phoneNum | true | string | 手机号 |
| smsCode | true | string | 短信验证码 |
| longtitude | true | string | 用户所处位置经度 |
| lantitude | true | string | 用户所处位置纬度 |

## 调用样例

---

```
user/login?phoneNum=18012345678smsCode=1234&longtitude=120&lantitude=40.2
```

## 成功返回结果

---

*** JSON示例 ***

```

{
accessToken: "f3ae42697ef6d67edb25d39adc3fe934"
}

```


关于其它错误返回值与错误代码，参见 [错误代码说明](#errorcode)
## 返回字段说明
---
|返回值字段 | 字段类型 | 字段说明 |
|:-------------|:-------------|:-------------|
| accessToken |  string | 用户凭证，代表唯一用户，具有操作权限 |


.
 
. 

## <span id = "user/follow">user/follow</span> [回到顶部](#backToTop)
---
关注某用户

## 支持格式

---

JSON
## HTTP请求方式

---

POST
## 请求参数
---
| | 必选 | 类型 | 说明 |
|:-------------|:-------------|:-------------|
| accessToken | true | string | 用户凭证 |
| followId | true | int64 | 要关注用户的id |


## 调用样例

---

```
user/follow?accessToken=cb57ca2ad7722fd8ec39c0327f7c8801&followId=1
```

## 成功返回结果

---

*** JSON示例 ***

```

{
status: 1
}

```


关于其它错误返回值与错误代码，参见 [错误代码说明](#errorcode)
## 返回字段说明
---
|返回值字段 | 字段类型 | 字段说明 |
|:-------------|:-------------|:-------------|
| status |  string | 状态，成功为 1 |

.
 
. 


## <span id = "user/cancle_follow">user/cancle_follow</span> [回到顶部](#backToTop)
---
取消关注某用户

## 支持格式

---

JSON
## HTTP请求方式

---

POST
## 请求参数
---
| | 必选 | 类型 | 说明 |
|:-------------|:-------------|:-------------|
| accessToken | true | string | 用户凭证 |
| followId | true | int64 | 要取消关注用户的id |


## 调用样例

---

```
user/cancle_follow?accessToken=cb57ca2ad7722fd8ec39c0327f7c8801&followId=1
```

## 成功返回结果

---

*** JSON示例 ***

```

{
status: 1
}

```


关于其它错误返回值与错误代码，参见 [错误代码说明](#errorcode)
## 返回字段说明
---
|返回值字段 | 字段类型 | 字段说明 |
|:-------------|:-------------|:-------------|
| status |  string | 状态，成功为 1 |

.
 
. 

## <span id = "user/modify_personal_info">user/modify_personal_info</span> [回到顶部](#backToTop)
---
修改个人信息

## 支持格式

---

JSON
## HTTP请求方式

---

POST
## 请求参数
---
| | 必选 | 类型 | 说明 |
|:-------------|:-------------|:-------------|
| accessToken | true | string | 用户凭证 |
| userNmae | false | string | 用户名 |
| description | false | string |  用户个性签名 |
| avatar | false | string | 用户头像图片地址 |


## 调用样例

---

```
user/modify_personal_info?accessToken=cb57ca2ad7722fd8ec39c0327f7c8801&userNmae=张三
```

## 成功返回结果

---

*** JSON示例 ***

```

{
user: {
avatar: "www.baidu.com",
createTime: 1462716192421,
description: "hello world",
dynamicCount: 7,
followersCount: 20,
friendsCount: 30,
id: 1,
lantitude: 40.5,
longtitude: 120.2,
phoneNum: "15659173545",
unreadCount: 5,
userName: "rush24"
}
}

```

关于其它错误返回值与错误代码，参见 [错误代码说明](#errorcode)
## 返回字段说明
---
|返回值字段 | 字段类型 | 字段说明 |
|:-------------|:-------------|:-------------|
| avatar |  string | 头像图片地址 |
| createTime |  int64 | 用户注册时间 |
| description |  string | 用户个性签名 |
| dynamicCount |  int | 用户发表过的动态数 |
| followersCount |  int | 用户关注者数量 |
| friendsCount |  int | 用户关注的人的数量 |
| id |  int64 | 用户id |
| lantitude |  string | 用户地理位置纬度 |
| longtitude |  string | 用户地理位置经度 |
| phoneNum |  string | 用户手机号 |
| unreadCount |  int | 用户消息未读数 |
| userName |  string | 用户名 |



.
 
. 

## <span id = "dynamic/timeline">dynamic/timeline</span> [回到顶部](#backToTop)
---
获取公共默认动态（按时间）

## 支持格式

---

JSON
## HTTP请求方式

---

GET
## 请求参数
---
| | 必选 | 类型 | 说明 |
|:-------------|:-------------|:-------------|
| accessToken | true | string | 用户凭证 |
| sinceId | false | int64 | 若指定此参数，则返回id比sinceId大的动态（即比sinceId时间晚的动态），默认为0。 |
| maxId | false | int64 | 若指定此参数，则返回id比maxId小的动态（不能同时制定sinceId和maxId,否则不返回结果） |


## 调用样例

---

```
dynamic/hot?accessToken=cb57ca2ad7722fd8ec39c0327f7c8801

```

## 成功返回结果

---

*** JSON示例 ***

```
{
dynamics: [
{
commentsCount: 0,
createTime: 1462809495402,
id: 33,
lantitude: 40.5,
likedCount: 0,
listenedCount: 0,
longtitude: 120.2,
text: "askcjsdv77",
user: {
avatar: "www.baidu.com",
createTime: 1462716192421,
description: "hello world",
dynamicCount: 7,
followersCount: 20,
friendsCount: 30,
id: 1,
lantitude: 40.5,
longtitude: 120.2,
phoneNum: "15659173545",
unreadCount: 5,
userName: "rush24"
},
voice: "www.xinlang.com",
voiceLength: 20
}
]
}
```

关于其它错误返回值与错误代码，参见 [错误代码说明](#errorcode)
## 返回字段说明
---
|返回值字段 | 字段类型 | 字段说明 |
|:-------------|:-------------|:-------------|
| commentsCount |  int | 该动态评论数量 |
| createTime |  int64 | 动态发表时间 |
| id |  int64 | 动态id |
| longtitude |  string | 动态发表所处地理位置经度 |
| lantitude |  string | 动态发表所处地理位置纬度 |
| likedCount | int | 动态被赞次数|
| listenedCount | int | 动态被听次数 |
| text |  string | 动态文字 |
| user | object |  动态所属用户 |
| voice | string |  动态声音文件地址 |
| voiceLength | int |  动态声音时长 |



.
 
. 

## <span id = "dynamic/hot">dynamic/hot</span> [回到顶部](#backToTop)
---
获取热门动态

## 支持格式

---

JSON
## HTTP请求方式

---

GET
## 请求参数
---
| | 必选 | 类型 | 说明 |
|:-------------|:-------------|:-------------|
| accessToken | true | string | 用户凭证 |
| sinceId | false | int64 | 若指定此参数，则返回id比sinceId大的动态（即比sinceId时间晚的动态），默认为0。 |
| maxId | false | int64 | 若指定此参数，则返回id比maxId小的动态（不能同时制定sinceId和maxId,否则不返回结果） |


## 调用样例

---

```
dynamic/timeline?accessToken=cb57ca2ad7722fd8ec39c0327f7c8801

```

## 成功返回结果

---

*** JSON示例 ***

```
{
dynamics: [
{
commentsCount: 0,
createTime: 1462809495402,
id: 33,
lantitude: 40.5,
likedCount: 0,
listenedCount: 0,
longtitude: 120.2,
text: "askcjsdv77",
user: {
avatar: "www.baidu.com",
createTime: 1462716192421,
description: "hello world",
dynamicCount: 7,
followersCount: 20,
friendsCount: 30,
id: 1,
lantitude: 40.5,
longtitude: 120.2,
phoneNum: "15659173545",
unreadCount: 5,
userName: "rush24"
},
voice: "www.xinlang.com",
voiceLength: 20
}
]
}
```

关于其它错误返回值与错误代码，参见 [错误代码说明](#errorcode)
## 返回字段说明
---
|返回值字段 | 字段类型 | 字段说明 |
|:-------------|:-------------|:-------------|
| commentsCount |  int | 该动态评论数量 |
| createTime |  int64 | 动态发表时间 |
| id |  int64 | 动态id |
| longtitude |  string | 动态发表所处地理位置经度 |
| lantitude |  string | 动态发表所处地理位置纬度 |
| likedCount | int | 动态被赞次数|
| listenedCount | int | 动态被听次数 |
| text |  string | 动态文字 |
| user | object |  动态所属用户 |
| voice | string |  动态声音文件地址 |
| voiceLength | int |  动态声音时长 |


.
 
. 

## <span id = "dynamic/nearby">dynamic/nearby</span> [回到顶部](#backToTop)
---
获取附近动态

## 支持格式

---

JSON
## HTTP请求方式

---

GET
## 请求参数
---
| | 必选 | 类型 | 说明 |
|:-------------|:-------------|:-------------|
| accessToken | true | string | 用户凭证 |
| user.longtitude | true | string | 用户所处地理经度 |
| user.lantitude | true | string | 用户所处地理纬度 |
| sinceId | false | int64 | 若指定此参数，则返回id比sinceId大的动态（即比sinceId时间晚的动态），默认为0。 |
| maxId | false | int64 | 若指定此参数，则返回id比maxId小的动态（不能同时制定sinceId和maxId,否则不返回结果） |


## 调用样例

---

```
dynamic/nearby?accessToken=cb57ca2ad7722fd8ec39c0327f7c8801&user.longtitude=110&user.lantitude=30

```

## 成功返回结果

---

*** JSON示例 ***

```
{
dynamics: [
{
commentsCount: 0,
createTime: 1462809495402,
id: 33,
lantitude: 40.5,
likedCount: 0,
listenedCount: 0,
longtitude: 120.2,
text: "askcjsdv77",
user: {
avatar: "www.baidu.com",
createTime: 1462716192421,
description: "hello world",
dynamicCount: 7,
followersCount: 20,
friendsCount: 30,
id: 1,
lantitude: 40.5,
longtitude: 120.2,
phoneNum: "15659173545",
unreadCount: 5,
userName: "rush24"
},
voice: "www.xinlang.com",
voiceLength: 20
}
]
}
```

关于其它错误返回值与错误代码，参见 [错误代码说明](#errorcode)
## 返回字段说明
---
|返回值字段 | 字段类型 | 字段说明 |
|:-------------|:-------------|:-------------|
| commentsCount |  int | 该动态评论数量 |
| createTime |  int64 | 动态发表时间 |
| id |  int64 | 动态id |
| longtitude |  string | 动态发表所处地理位置经度 |
| lantitude |  string | 动态发表所处地理位置纬度 |
| likedCount | int | 动态被赞次数|
| listenedCount | int | 动态被听次数 |
| text |  string | 动态文字 |
| user | object |  动态所属用户 |
| voice | string |  动态声音文件地址 |
| voiceLength | int |  动态声音时长 |



.
 
. 

## <span id = "dynamic/recommend">dynamic/recommend</span> [回到顶部](#backToTop)
---
获取猜你喜欢动态

## 支持格式

---

JSON
## HTTP请求方式

---

GET
## 请求参数
---
| | 必选 | 类型 | 说明 |
|:-------------|:-------------|:-------------|
| accessToken | true | string | 用户凭证 |
| sinceId | false | int64 | 若指定此参数，则返回id比sinceId大的动态（即比sinceId时间晚的动态），默认为0。 |
| maxId | false | int64 | 若指定此参数，则返回id比maxId小的动态（不能同时制定sinceId和maxId,否则不返回结果） |


## 调用样例

---

```
dynamic/recommend?accessToken=cb57ca2ad7722fd8ec39c0327f7c8801
```

## 成功返回结果

---

*** JSON示例 ***

```
{
dynamics: [
{
commentsCount: 0,
createTime: 1462809495402,
id: 33,
lantitude: 40.5,
likedCount: 0,
listenedCount: 0,
longtitude: 120.2,
text: "askcjsdv77",
user: {
avatar: "www.baidu.com",
createTime: 1462716192421,
description: "hello world",
dynamicCount: 7,
followersCount: 20,
friendsCount: 30,
id: 1,
lantitude: 40.5,
longtitude: 120.2,
phoneNum: "15659173545",
unreadCount: 5,
userName: "rush24"
},
voice: "www.xinlang.com",
voiceLength: 20
}
]
}
```

关于其它错误返回值与错误代码，参见 [错误代码说明](#errorcode)
## 返回字段说明
---
|返回值字段 | 字段类型 | 字段说明 |
|:-------------|:-------------|:-------------|
| commentsCount |  int | 该动态评论数量 |
| createTime |  int64 | 动态发表时间 |
| id |  int64 | 动态id |
| longtitude |  string | 动态发表所处地理位置经度 |
| lantitude |  string | 动态发表所处地理位置纬度 |
| likedCount | int | 动态被赞次数|
| listenedCount | int | 动态被听次数 |
| text |  string | 动态文字 |
| user | object |  动态所属用户 |
| voice | string |  动态声音文件地址 |
| voiceLength | int |  动态声音时长 |


.
 
. 

## <span id = "dynamic/friends">dynamic/friends</span> [回到顶部](#backToTop)
---
获取关注好友发表的动态

## 支持格式

---

JSON
## HTTP请求方式

---

GET
## 请求参数
---
| | 必选 | 类型 | 说明 |
|:-------------|:-------------|:-------------|
| accessToken | true | string | 用户凭证 |
| sinceId | false | int64 | 若指定此参数，则返回id比sinceId大的动态（即比sinceId时间晚的动态），默认为0。 |
| maxId | false | int64 | 若指定此参数，则返回id比maxId小的动态（不能同时制定sinceId和maxId,否则不返回结果） |


## 调用样例

---

```
dynamic/friends?accessToken=cb57ca2ad7722fd8ec39c0327f7c8801
```

## 成功返回结果

---

*** JSON示例 ***

```
{
dynamics: [
{
commentsCount: 0,
createTime: 1462809495402,
id: 33,
lantitude: 40.5,
likedCount: 0,
listenedCount: 0,
longtitude: 120.2,
text: "askcjsdv77",
user: {
avatar: "www.baidu.com",
createTime: 1462716192421,
description: "hello world",
dynamicCount: 7,
followersCount: 20,
friendsCount: 30,
id: 1,
lantitude: 40.5,
longtitude: 120.2,
phoneNum: "15659173545",
unreadCount: 5,
userName: "rush24"
},
voice: "www.xinlang.com",
voiceLength: 20
}
]
}
```

关于其它错误返回值与错误代码，参见 [错误代码说明](#errorcode)
## 返回字段说明
---
|返回值字段 | 字段类型 | 字段说明 |
|:-------------|:-------------|:-------------|
| commentsCount |  int | 该动态评论数量 |
| createTime |  int64 | 动态发表时间 |
| id |  int64 | 动态id |
| longtitude |  string | 动态发表所处地理位置经度 |
| lantitude |  string | 动态发表所处地理位置纬度 |
| likedCount | int | 动态被赞次数|
| listenedCount | int | 动态被听次数 |
| text |  string | 动态文字 |
| user | object |  动态所属用户 |
| voice | string |  动态声音文件地址 |
| voiceLength | int |  动态声音时长 |

.
 
. 

## <span id = "dynamic/history">dynamic/history</span> [回到顶部](#backToTop)
---
获取某用户发表过的动态

## 支持格式

---

JSON
## HTTP请求方式

---

GET
## 请求参数
---
| | 必选 | 类型 | 说明 |
|:-------------|:-------------|:-------------|
| accessToken | true | string | 用户凭证 |
| searchUserId | true | int64 | 要查询的用户id |
| sinceId | false | int64 | 若指定此参数，则返回id比sinceId大的动态（即比sinceId时间晚的动态），默认为0。 |
| maxId | false | int64 | 若指定此参数，则返回id比maxId小的动态（不能同时制定sinceId和maxId,否则不返回结果） |


## 调用样例

---

```
dynamic/history?accessToken=cb57ca2ad7722fd8ec39c0327f7c8801&searchUserId=1
```

## 成功返回结果

---

*** JSON示例 ***

```
{
dynamics: [
{
commentsCount: 0,
createTime: 1462809495402,
id: 33,
lantitude: 40.5,
likedCount: 0,
listenedCount: 0,
longtitude: 120.2,
text: "askcjsdv77",
user: {
avatar: "www.baidu.com",
createTime: 1462716192421,
description: "hello world",
dynamicCount: 7,
followersCount: 20,
friendsCount: 30,
id: 1,
lantitude: 40.5,
longtitude: 120.2,
phoneNum: "15659173545",
unreadCount: 5,
userName: "rush24"
},
voice: "www.xinlang.com",
voiceLength: 20
}
]
}
```

关于其它错误返回值与错误代码，参见 [错误代码说明](#errorcode)
## 返回字段说明
---
|返回值字段 | 字段类型 | 字段说明 |
|:-------------|:-------------|:-------------|
| commentsCount |  int | 该动态评论数量 |
| createTime |  int64 | 动态发表时间 |
| id |  int64 | 动态id |
| longtitude |  string | 动态发表所处地理位置经度 |
| lantitude |  string | 动态发表所处地理位置纬度 |
| likedCount | int | 动态被赞次数|
| listenedCount | int | 动态被听次数 |
| text |  string | 动态文字 |
| user | object |  动态所属用户 |
| voice | string |  动态声音文件地址 |
| voiceLength | int |  动态声音时长 |


.
 
. 

## <span id = "dynamic/listen">dynamic/listen</span> [回到顶部](#backToTop)
---
听一条动态

## 支持格式

---

JSON
## HTTP请求方式

---

POST
## 请求参数
---
| | 必选 | 类型 | 说明 |
|:-------------|:-------------|:-------------|
| accessToken | true | string | 用户凭证 |
| id | true | int64 | 听的动态id |


## 调用样例

---

```
user/listen?accessToken=cb57ca2ad7722fd8ec39c0327f7c8801&id=1
```

## 成功返回结果

---

*** JSON示例 ***

```

{
status: 1
}

```


关于其它错误返回值与错误代码，参见 [错误代码说明](#errorcode)
## 返回字段说明
---
|返回值字段 | 字段类型 | 字段说明 |
|:-------------|:-------------|:-------------|
| status |  string | 状态，成功为 1 |


.
 
. 

## <span id = "dynamic/publish">dynamic/publish</span> [回到顶部](#backToTop)
---
发表一条动态

## 支持格式

---

JSON
## HTTP请求方式

---

POST
## 请求参数
---
| | 必选 | 类型 | 说明 |
|:-------------|:-------------|:-------------|
| accessToken | true | string | 用户凭证 |
| text | true | string | 动态文字 |
| voice | true | string | 动态语音地址 |
| voicelength | true | int | 动态语音长度 |
| longtitude | true | string | 动态发表位置经度 |
| lantitude | true | string |动态发表位置纬度 |

## 调用样例

---

```
dynamic/publish?accessToken=cb57ca2ad7722fd8ec39c0327f7c8801&text=你好世界&voice=www.xinalng.com&voiceLength=60&longtitude=120&lantitude=30
```

## 成功返回结果

---

*** JSON示例 ***

```

{
commentsCount: 0,
createTime: 1463552404727,
id: 34,
lantitude: 30,
likedCount: 0,
listenedCount: 0,
longtitude: 120,
text: "你好世界",
user: {
avatar: "www.baidu.com",
createTime: 1462716192421,
description: "hello world",
dynamicCount: 8,
followersCount: 20,
friendsCount: 30,
id: 1,
lantitude: 30,
longtitude: 120,
phoneNum: "15659173545",
unreadCount: 5,
userName: "rush24"
},
voice: "www.xinalng.com",
voiceLength: 60
}

```


关于其它错误返回值与错误代码，参见 [错误代码说明](#errorcode)
## 返回字段说明
---
|返回值字段 | 字段类型 | 字段说明 |
|:-------------|:-------------|:-------------|
| commentsCount |  int | 该动态评论数量 |
| createTime |  int64 | 动态发表时间 |
| id |  int64 | 动态id |
| longtitude |  string | 动态发表所处地理位置经度 |
| lantitude |  string | 动态发表所处地理位置纬度 |
| likedCount | int | 动态被赞次数|
| listenedCount | int | 动态被听次数 |
| text |  string | 动态文字 |
| user | object |  动态所属用户 |
| voice | string |  动态声音文件地址 |
| voiceLength | int |  动态声音时长 |


.
 
. 

## <span id = "dynamic/delete">dynamic/delete</span> [回到顶部](#backToTop)
---
删除一条动态

## 支持格式

---

JSON
## HTTP请求方式

---

POST
## 请求参数
---
| | 必选 | 类型 | 说明 |
|:-------------|:-------------|:-------------|
| accessToken | true | string | 用户凭证 |
| id | true | int64 | 要删除的动态id |


## 调用样例

---

```
user/delete?accessToken=cb57ca2ad7722fd8ec39c0327f7c8801&id=1
```

## 成功返回结果

---

*** JSON示例 ***

```

{
status: 1
}

```


关于其它错误返回值与错误代码，参见 [错误代码说明](#errorcode)
## 返回字段说明
---
|返回值字段 | 字段类型 | 字段说明 |
|:-------------|:-------------|:-------------|
| status |  string | 状态，成功为 1 |


.
 
. 

## <span id = "comment/comments">comment/comments</span> [回到顶部](#backToTop)
---
获取某一条动态的评论

## 支持格式

---

JSON
## HTTP请求方式

---

GET
## 请求参数
---
| | 必选 | 类型 | 说明 |
|:-------------|:-------------|:-------------|
| accessToken | true | string | 用户凭证 |
| dynamic.id | true | int64 | 要查看的动态id |
| sinceId | false | int64 | 若指定此参数，则返回id比sinceId大的评论（即比sinceId时间晚的评论），默认为0。 |
| maxId | false | int64 | 若指定此参数，则返回id比maxId小的评论（不能同时制定sinceId和maxId,否则不返回结果） |

## 调用样例

---

```
comment/comments?accessToken=cb57ca2ad7722fd8ec39c0327f7c8801&dynamic.id=1
```

## 成功返回结果

---

*** JSON示例 ***

```

{
comments: [
{
createTime: 0,
dynamic: {
commentsCount: 1,
createTime: 1463495747951,
id: 4,
lantitude: 30.1,
likedCount: 1,
listenedCount: 2,
longtitude: 110.1,
text: "44",
user: {
avatar: "",
createTime: 0,
description: "",
dynamicCount: 0,
followersCount: 0,
friendsCount: 0,
id: 2,
lantitude: 41,
longtitude: 121,
phoneNum: "",
unreadCount: 0,
userName: "ru"
},
voice: "",
voiceLength: 0
},
id: 2,
replyComment: null,
text: "11",
type: 0,
user: {
avatar: "",
createTime: 0,
description: "",
dynamicCount: 0,
followersCount: 0,
friendsCount: 0,
id: 2,
lantitude: 41,
longtitude: 121,
phoneNum: "",
unreadCount: 0,
userName: "ru"
},
voice: "ww",
voiceLength: 12
}
]
}

```


关于其它错误返回值与错误代码，参见 [错误代码说明](#errorcode)
## 返回字段说明
---
|返回值字段 | 字段类型 | 字段说明 |
|:-------------|:-------------|:-------------|
| createTime |  int64 | 评论发表时间 |
| dynamic |  object | 评论所属动态 |
| id |  int64 | 评论id |
| replyComment |  object | 评论来源评论 |
| text |  string | 评论文字 |
| type |  string | 评论类型，0 为普通评论，1 为赞 |
| user | object |  评论所属用户 |
| voice | string |  评论声音文件地址 |
| voiceLength | int |  评论声音时长 |


.
 
. 

## <span id = "comment/to_me">comment/to_me</span> [回到顶部](#backToTop)
---
获取某个用户收到的评论

## 支持格式

---

JSON
## HTTP请求方式

---

GET
## 请求参数
---
| | 必选 | 类型 | 说明 |
|:-------------|:-------------|:-------------|
| accessToken | true | string | 用户凭证 |
| sinceId | false | int64 | 若指定此参数，则返回id比sinceId大的评论（即比sinceId时间晚的评论），默认为0。 |
| maxId | false | int64 | 若指定此参数，则返回id比maxId小的评论（不能同时制定sinceId和maxId,否则不返回结果） |

## 调用样例

---

```
comment/to_me?accessToken=cb57ca2ad7722fd8ec39c0327f7c8801

```

## 成功返回结果

---

*** JSON示例 ***

```

{
comments: [
{
createTime: 0,
dynamic: {
commentsCount: 1,
createTime: 1463495747951,
id: 4,
lantitude: 30.1,
likedCount: 1,
listenedCount: 2,
longtitude: 110.1,
text: "44",
user: {
avatar: "",
createTime: 0,
description: "",
dynamicCount: 0,
followersCount: 0,
friendsCount: 0,
id: 2,
lantitude: 41,
longtitude: 121,
phoneNum: "",
unreadCount: 0,
userName: "ru"
},
voice: "",
voiceLength: 0
},
id: 2,
replyComment: null,
text: "11",
type: 0,
user: {
avatar: "",
createTime: 0,
description: "",
dynamicCount: 0,
followersCount: 0,
friendsCount: 0,
id: 2,
lantitude: 41,
longtitude: 121,
phoneNum: "",
unreadCount: 0,
userName: "ru"
},
voice: "ww",
voiceLength: 12
}
]
}

```


关于其它错误返回值与错误代码，参见 [错误代码说明](#errorcode)
## 返回字段说明
---
|返回值字段 | 字段类型 | 字段说明 |
|:-------------|:-------------|:-------------|
| createTime |  int64 | 评论发表时间 |
| dynamic |  object | 评论所属动态 |
| id |  int64 | 评论id |
| replyComment |  object | 评论来源评论 |
| text |  string | 评论文字 |
| type |  string | 评论类型，0 为普通评论，1 为赞 |
| user | object |  评论所属用户 |
| voice | string |  评论声音文件地址 |
| voiceLength | int |  评论声音时长 |


.
 
. 

## <span id = "comment/create">comment/create</span> [回到顶部](#backToTop)
---
评论

## 支持格式

---

JSON
## HTTP请求方式

---

POST
## 请求参数
---
| | 必选 | 类型 | 说明 |
|:-------------|:-------------|:-------------|
| accessToken | true | string | 用户凭证 |
| dynamic.id | true | int64 | 要评论的动态 |
| type | true | string | 评论类型 |
| text | false | string | 评论文字 |
| voice | false | string | 评论声音 |
| voiceLength | false | string | 评论声音长度 |
| replyComment.id | fasle | string | 来源评论id |
## 调用样例

---

```
comment/create?accessToken=cb57ca2ad7722fd8ec39c0327f7c8801&dynamic.id=1&type=0

```

## 成功返回结果

---

*** JSON示例 ***

```

{
status: 1
}

```


关于其它错误返回值与错误代码，参见 [错误代码说明](#errorcode)
## 返回字段说明
---
|返回值字段 | 字段类型 | 字段说明 |
|:-------------|:-------------|:-------------|
| status |  string | 状态，成功为 1 |


.
 
. 

## <span id = "comment/delete">comment/delete</span> [回到顶部](#backToTop)
---
删除评论

## 支持格式

---

JSON
## HTTP请求方式

---

POST
## 请求参数
---
| | 必选 | 类型 | 说明 |
|:-------------|:-------------|:-------------|
| accessToken | true | string | 用户凭证 |
| id | true | int64 | 评论id |
## 调用样例

---

```
/comment/delete?accessToken=cb57ca2ad7722fd8ec39c0327f7c8801&id=12

```

## 成功返回结果

---

*** JSON示例 ***

```

{
status: 1
}

```


关于其它错误返回值与错误代码，参见 [错误代码说明](#errorcode)
## 返回字段说明
---
|返回值字段 | 字段类型 | 字段说明 |
|:-------------|:-------------|:-------------|
| status |  string | 状态，成功为 1 |


# <span id = "errorcode">ErrorCode</span>
### 错误返回结果
---
JSON示例

```
{
errorCode: "2109",
error: "phoneNum already exits"
}

```
### 错误代码对照表[回到顶部](#backToTop)
---
##### 系统级错误
---
| 错误代码 | 返回msg | 详细描述 |
|:-------------:|:-------------|
| | | |


##### 业务级错误
---
| 错误代码 | 详细描述 |
|:-------------:|:-------------|
|2001|phoneNum is null
|2002|userName is null
|2003|smsCode is null
|2004|accessToken is null
|2005|searchKeyword is null
|2006|followId is null
|2007|uploadToken is null
|2008|searchUserId is null
|2009|longtitude and lantitude should be not null
|2010|userId is null
|2011|dynamicId is null
|2012|dynamicText is null
|2013|dynamicVoice is null
|2014|longtitude and lantitude should be not null
|2015|dynamicVoiceLength is null
|2016|commentType is null
|2017|commentId is null
|2100|accessToken is wrong
|2101|userId isn't exit
|2102|followUser isn't exit
|2103|searchUser isn't exit
|2104|dynamicText length is too long
|2105|smsCode is wrong
|2106|it's not your comment
|2107|dynamic isn't exit
|2108|it's not your dynamic
|2109|phoneNum already exits
|2110|userNmae already exits
|2111|userNmae or phoneNum already exits
|2112|you haven't followed him/her
|2113|voiceLength is too long
