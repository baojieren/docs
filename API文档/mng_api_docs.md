# 管理系统接口

版本号|修改人|修改时间|修改项
:---|:---|:---|:---
1.0|任宝杰|2019-6-27|初版

## 登陆注册

>### 登录

接口用途:   
接口鉴权: 否  
测试地址: https://api.baojie.ink/xmg/login  
正式地址: https://api.baojie.ink/xmg/login  
请求方式: POST  
请求参数:
```json
{
	"phone":"18585131312",
	"password":"142536"
}
```
返回结果:
```json
{
    "code": 0,
    "msg": "成功",
    "data": {
        "userId": 1,
        "phone": "18585131312",
        "userName": "baojieren",
        "image": "\"\"",
        "token": "SESS18585131312",
        "roleList": [
            {
                "roleTag": "admin",
                "roleTitle": "超管"
            }
        ]
    }
}
```

>### 注册

接口用途:   
接口鉴权: 否  
测试地址: https://api.baojie.ink/xmg/signUp  
正式地址: https://api.baojie.ink/xmg/signUp  
请求方式: POST  
请求参数:
```json
{
  "phone": "18585131312",
  "password": "123456",
  "userName": "baojieren"
}
```
返回结果:
```json
{
    "code": 0,
    "msg": "成功"
}
```

>### 修改密码

接口用途:   
接口鉴权: 是  
测试地址: https://api.baojie.ink/xmg/updatePass  
正式地址: https://api.baojie.ink/xmg/updatePass  
请求方式: POST  
请求参数:
```json
{
	"phone":"18585131312",
	"password":"142536" //新密码
}
```
返回结果:
```json
{
    "code": 0,
    "msg": "成功"
}
```

>### 修改资料

接口用途:   
接口鉴权: 是  
测试地址: https://api.baojie.ink/xmg/update  
正式地址: https://api.baojie.ink/xmg/update  
请求方式: POST  
请求参数:
```json
{
    "id": 1, //userId
	"phone":"18585131312", //新手机号
	"userName":"baojierne" //新用户名
}
```
返回结果:
```json
{
    "code": 0,
    "msg": "成功"
}
```

>### 退出登录

接口用途:   
接口鉴权: 是  
测试地址: https://api.baojie.ink/xmg/logout  
正式地址: https://api.baojie.ink/xmg/logout  
请求方式: POST  
请求参数:
```
null
```
返回结果:
```json
{
    "code": 0,
    "msg": "成功"
}
```

## 用户中心

>### 查询用户列表

接口用途:   
接口鉴权: 否  
测试地址: https://api.baojie.ink/xmg/user/list  
正式地址: https://api.baojie.ink/xmg/user/list  
请求方式: POST  
请求参数:
```json
{
    "pageIndex": 1, //页码,默认为1 
    "pageSize": 15, //每页大小,默认为15
    "startTime": "2019-05-25 12:57:05", //结束时间
    "endTime": "2019-05-25 12:57:05", //开始日期
    "userName": "baojie", //用户名,支持模糊搜索
    "phone": "18585131312" //完整手机号
}
```
返回结果:
```json
{
    "code": 0,
    "msg": "成功",
    "data": {
        "total": 1, //总记录数
        "list": [
            {
                "id": 1, //用户id
                "userName": "baojieren", //用户名
                "phone": "18585131312",
                "password": "222222",
                "schoolId": null,
                "teamId": null, //班级id
                "openId": "123456789",
                "wxId": "18585131312",
                "image": "", //头像
                "birthday": null, //生日
                "sex": 0, //0:男生,1:女生
                "vip": 0,
                "vipStatus": 0, //0:VIP无效,1:VIP有效
                "vipStart": null, //开通vip时间
                "vipEnd": null, //vip到期时间
                "score": 0,
                "inviteCode": "",
                "valid": 1,
                "createTime": "2019-06-25T00:57:07", //会员注册时间
                "updateTime": "2019-06-27T07:44:14"
            }
        ]
    }
}
```

## 题库中心

>### 获取上传图片token

接口用途:   
接口鉴权: 是  
测试地址: https://api.baojie.ink/xmg/img/token  
正式地址: https://api.baojie.ink/xmg/img/token  
请求方式: GET  
请求参数:
```
fileName=aaa.png //图片名称
```
返回结果:
```json
{
    "code": 0,
    "msg": "成功",
    "data": {
        "domain": "https://upload-z2.qiniup.com", //图片上传地址
        "token": "Ki7rB" //token
    }
}
```

>### 上传题目

接口用途:   
接口鉴权: 否  
测试地址: https://api.baojie.ink/xmg/quest/save  
正式地址: https://api.baojie.ink/xmg/quest/save  
请求方式: POST  
请求参数:
```json
{
    "owner": 1, //上传者id
    "name": "2 X 2 = 5 对吗?", //题干
    "quesKey": "1", //正确答案(eg:选择题:"A",判断题:"0":对,"1":错,填空题:"5")
    "analysis": "正确答案是4啊", //题目解析
    "limitTime": 20, //做题时长(秒)
    "difficult": 0, //0:简单,1:中等,2:困难
    "answerType": 1, //0:选择题,1:判断题,2:填空题
    "natureType": 0, //0:基础题,1:概念题,2:综合题
    "option": [{ "key": "A", "value": "12" }, { "key": "B", "value": "20" }], //只有选择题才填该字段
    "unitId": 1, //该题目属于哪个单元id
    "knowledgeId": 1 //该题目属于哪个知识点id
}
```
返回结果:
```json
{
    "code": 0,
    "msg": "成功",
    "data": null
}
```

>### 删除题目

接口用途:   
接口鉴权: 否  
测试地址: https://api.baojie.ink/xmg/quest/delete  
正式地址: https://api.baojie.ink/xmg/quest/delete  
请求方式: GET  
请求参数:
```json
id=2
```
返回结果:
```json
{
    "code": 0,
    "msg": "成功",
    "data": null
}
```

>### 根据id查询题目

接口用途:   
接口鉴权: 否  
测试地址: https://api.baojie.ink/xmg/quest/one  
正式地址: https://api.baojie.ink/xmg/quest/one  
请求方式: GET  
请求参数:
```json
id=2
```
返回结果:
```json
{
    "code": 0,
    "msg": "成功",
    "data": {
        "id": 8,
        "owner": 1,
        "name": "修改8",
        "quesKey": "A",
        "analysis": "分析",
        "limitTime": 10,
        "difficult": 0,
        "answerType": 0,
        "natureType": 0,
        "option": [
            {
                "key": "A",
                "value": "12"
            },
            {
                "key": "B",
                "value": "20"
            }
        ],
        "unitId": 1,
        "knowledgeId": 1,
        "remark": ""
    }
}
```

>### 根据id修改题目

接口用途:   
接口鉴权: 否  
测试地址: https://api.baojie.ink/xmg/quest/update  
正式地址: https://api.baojie.ink/xmg/quest/update  
请求方式: POST  
请求参数:
```json
{
    "id":2,
    "owner": 1,
    "name": "4+2等于()",
    "quesKey": "6",
    "analysis": "正确答案是6啊",
    "limitTime": 20,
    "difficult": 0,
    "answerType": 2,
    "natureType": 0,
    "option": [],
    "unitId": 1,
    "knowledgeId": 1
}
```
返回结果:
```json
{
    "code": 0,
    "msg": "成功",
    "data": null
}
```

>### 查询题目列表

接口用途:   
接口鉴权: 否  
测试地址: https://api.baojie.ink/xmg/quest/list  
正式地址: https://api.baojie.ink/xmg/quest/list  
请求方式: POST  
请求参数:
```json
{
  "startTime": "", //开始时间
  "endTime": "", //结束时间
  "name": "", //题目名称,支持模糊
  "difficult": 1, //0:简单,1:中等,2:困难
  "answerType": 1, //0:选择题,1:判断题,2:填空题
  "natureType": 1, //0:基础题,1:概念题,2:综合题
  "valid": 1 //0:无效，1:审核中 , 2:审核失败 , 3:审核成功
}
```
返回结果:
```json
{
    "code": 0,
    "msg": "成功",
    "data": {
        "total": 1,
        "list": [
            {
                "phone": "18585131312", //上传者手机
                "id": 4, //题目id
                "owner": 1, 上传者id
                "name": "2 X 2 = 5 对吗?", //题干
                "quesKey": "错", //题目正确答案
                "analysis": "正确答案是4啊", //歇息
                "limitTime": 20, //做题时间
                "difficult": 0,
                "answerType": 1,
                "natureType": 0,
                "option": null, //选择题的选项
                "knowledge": "小数点移位", //知识点名称
                "remark": "", //备注
                "reviewDes": "", //审核说明
                "valid": 0, //0:无效，1:审核中 , 2:审核失败 , 3:审核成功
                "reviewDate": null, //审核日期
                "reviewTime": null, //审核时间
                "createTime": "2019-06-30 12:07:24" //题目创建时间
            }
        ]
    }
}
```

>### 审核题目

接口用途:   
接口鉴权: 是  
测试地址: https://api.baojie.ink/xmg/quest/review  
正式地址: https://api.baojie.ink/xmg/quest/review  
请求方式: POST  
请求参数:
```json
{
  "id": 8, //题目id
  "reviewDes": "不过", //审核说明
  "valid": 2 //2:审核不通过 , 3:审核通过
}
```
返回结果:
```json
{
    "code": 0,
    "msg": "成功",
    "data": null
}
```