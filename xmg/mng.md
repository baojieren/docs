# 管理系统接口

版本号|修改人|修改时间|修改项
:---|:---|:---|:---
1.0|任宝杰|2019-6-27|初版

# 鉴权步骤
1. 先登陆,后台使用手机号+密码方式登陆,小程序使用openId登陆
2. 登陆成功获得token
3. 以后每次请求接口在请求头携带token标识
4. 请求头token格式: Authorization: Bearer token   //Bearer为固定标识，空格后接token串

# 登陆注册

## 后台老师扫码获取openId
接口用途:   
接口鉴权: 否  
测试地址: https://api.baojie.ink/xmg/openId/mng  
正式地址: https://api.baojie.ink/xmg/openId/mng  
请求方式: GET  
请求参数:
```
code="asdfg"
```
返回结果:
```
{
  "code": 0,
  "msg": "成功",
  "data": null
}
```

## 注册
接口用途:   
接口鉴权: 否  
测试地址: https://api.baojie.ink/xmg/signUp  
正式地址: https://api.baojie.ink/xmg/signUp  
请求方式: POST  
请求参数:
```
{
  "phone": "18585131312",
  "password": "123456",
  "userName": "baojieren",
  "openId": "dsaeadsagdsa"
}
```
返回结果:
```
{
    "code": 0,
    "msg": "成功"
}
```

## 登录
接口用途:   
接口鉴权: 否  
测试地址: https://api.baojie.ink/xmg/login  
正式地址: https://api.baojie.ink/xmg/login  
请求方式: POST  
请求参数:
```
{
	"phone":"18585131312",
	"password":"142536"
}
```
返回结果:
```
{
    "code": 0,
    "msg": "成功",
    "data": {
        "userId": 1,
        "phone": "18585131312",
        "userName": "baojieren",
        "image": "",
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

## 修改密码
接口用途:   
接口鉴权: 是  
测试地址: https://api.baojie.ink/xmg/updatePass  
正式地址: https://api.baojie.ink/xmg/updatePass  
请求方式: POST  
请求参数:
```
{
	"phone":"18585131312",
	"password":"142536" //新密码
}
```
返回结果:
```
{
    "code": 0,
    "msg": "成功"
}
```

## 修改资料
接口用途:   
接口鉴权: 是  
测试地址: https://api.baojie.ink/xmg/update  
正式地址: https://api.baojie.ink/xmg/update  
请求方式: POST  
请求参数:
```
{
    "id": 1, //userId
	"phone":"18585131312", //新手机号
	"userName":"baojierne" //新用户名
}
```
返回结果:
```
{
    "code": 0,
    "msg": "成功"
}
```

## 退出登录
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
```
{
    "code": 0,
    "msg": "成功"
}
```

# 后台首页

## 首页老师概览
接口用途:   
接口鉴权: 是  
测试地址: https://api.baojie.ink/xmg/user/overview  
正式地址: https://api.baojie.ink/xmg/user/overview  
请求方式: GET  
请求参数:
```
id=2
```
返回结果:
```
{
    "code": 0,
    "msg": "成功",
    "data": {
        "userName": "任宝杰", //用户名
        "passNum": 6, //通过的题目数
        "usedNum": 3 //被使用的题目数
    }
}
```

## 查询用户列表
接口用途:   
接口鉴权: 否  
测试地址: https://api.baojie.ink/xmg/user/list  
正式地址: https://api.baojie.ink/xmg/user/list  
请求方式: POST  
请求参数:
```
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
```
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

# 题库中心

## 题库中心概览
接口用途:   
接口鉴权: 是  
测试地址: https://api.baojie.ink/xmg/quest/allOverview  
正式地址: https://api.baojie.ink/xmg/quest/allOverview  
请求方式: GET  
请求参数:
```
null
```
返回结果:
```
{
    "code": 0,
    "msg": "成功",
    "data": {
        "total": 0,
        "list": [
            {
                "gradeName": "六年级", //年级名称
                "bookName": "六年级数学上册", //教材名称
                "unitNum": 1, //单元数量
                "knowledgeNum": 1, //知识点数量
                "simpleNum": 6, //总的简单题数
                "simplePassNum": 5, //通过审核的简单题数
                "mediumNum": 0, //总的中等题数
                "mediumPassNum": 0, //通过审核的中等题数量
                "hardNum": 0, //总的困难题数
                "hardPassNum": 0 //通过审核的困难题数量
            },
            {
                "gradeName": "六年级",
                "bookName": "六年级英语下册",
                "unitNum": 2,
                "knowledgeNum": 1,
                "simpleNum": 0,
                "simplePassNum": 0,
                "mediumNum": 0,
                "mediumPassNum": 0,
                "hardNum": 1,
                "hardPassNum": 1
            }
        ]
    }
}
```

## 获取所有的年级列表
接口用途:   
接口鉴权: 是  
测试地址: https://api.baojie.ink/xmg/{mini}/grade/all  
正式地址: https://api.baojie.ink/xmg/{mini}/grade/all  
请求方式: GET  
请求参数:
```
null
```
返回结果:
```
{
    "code": 0,
    "msg": "成功",
    "data": {
        "total": 1,
        "list": [
            {
                "id": 3, //年级id
                "gradeName": "三年级", //年级名称
                "gradeDes": "湖南小学三年级", // 年级描述
                "valid": 1, //0无效，1有效
                "createTime": "2019-06-30 11:11:38",
                "updateTime": "2019-06-30 11:13:04"
            }
        ]
    }
}
```

## 根据年级id获取教材列表
接口用途:   
接口鉴权: 是  
测试地址: https://api.baojie.ink/xmg/{mini}/book/listByGradeId  
正式地址: https://api.baojie.ink/xmg/{mini}/book/listByGradeId  
请求方式: GET  
请求参数:
```
gradeId=6
```
返回结果:
```
{
    "code": 0,
    "msg": "成功",
    "data": {
        "total": 2,
        "list": [
            {
                "id": 1, //册id
                "bookName": "六年级数学上册", //书名
                "bookDes": "湖南小学六年级数学上册", //书描述
                "gradeId": 6, //年级id
                "valid": 1, //0无效，1有效
                "createTime": "2019-06-30 09:32:56",
                "updateTime": "2019-06-30 11:15:40"
            },
            {
                "id": 2,
                "bookName": "六年级英语下册",
                "bookDes": "湖南小学",
                "gradeId": 6,
                "valid": 1,
                "createTime": "2019-07-04 13:43:13",
                "updateTime": "2019-07-04 13:43:13"
            }
        ]
    }
}
```

## 根据教材id获取单元列表
接口用途:   
接口鉴权: 是  
测试地址: https://api.baojie.ink/xmg/{mini}/unit/listByBookId  
正式地址: https://api.baojie.ink/xmg/{mini}/unit/listByBookId  
请求方式: GET  
请求参数:
```
bookId=1
```
返回结果:
```
{
    "code": 0,
    "msg": "成功",
    "data": {
        "total": 0,
        "list": [
            {
                "id": 1, //单元id
                "unitName": "小数乘法", //单元名称
                "unitDes": "湖南小学六年级数学上册小数乘法", //单元描述
                "bookId": 1, //册id
                "valid": 1, //0无效，1有效
                "createTime": "2019-06-30 09:33:33",
                "updateTime": "2019-06-30 11:16:09"
            }
        ]
    }
}
```

## 根据单元id获取知识点列表
接口用途:   
接口鉴权: 是  
测试地址: https://api.baojie.ink/xmg/{mini}/knowledge/listByUnitId  
正式地址: https://api.baojie.ink/xmg/{mini}/knowledge/listByUnitId  
请求方式: GET  
请求参数:
```
unitId=1
```
返回结果:
```
{
    "code": 0,
    "msg": "成功",
    "data": {
        "total": 0,
        "list": [
            {
                "id": 1, //知识点id
                "knowledgeName": "小数点移位", //知识点名称
                "unitId": 1, //单元id
                "totalQuestNum": 6, //总题目数
                "passQuestNum": 5 //通过审核的题目数
            }
        ]
    }
}
```

## 获取所有知识点列表
接口用途:   
接口鉴权: 是  
测试地址: https://api.baojie.ink/xmg/knowledge/all  
正式地址: https://api.baojie.ink/xmg/knowledge/all  
请求方式: GET  
请求参数:
```
null
```
返回结果:
```
{
  "code": 0,
  "msg": "成功",
  "data": [
    {
      "id": 1,
      "knowledgeName": "小数点移位", //知识点名称
      "knowledgeDes": "湖南小学六年级数学上册小数乘法小数点移位" //知识点描述
    },
    {
      "id": 2,
      "knowledgeName": "主谓宾",
      "knowledgeDes": "湖南小学"
    }
  ]
}
```

## 根据知识点id获取题目数
接口用途:   
接口鉴权: 是  
测试地址: https://api.baojie.ink/xmg/type/diffcult  
正式地址: https://api.baojie.ink/xmg/type/diffcult  
请求方式: GET  
请求参数:
```
knowledgeId=1
```
返回结果:
```
{
    "code": 0,
    "msg": "成功",
    "data": [
        {
            "difficult": 0, //0:简单,1:中等,2:困难
            "totalQuestSum": 7, //题目总数
            "passQuestSum": 2 //审核通过数
        },
        {
            "difficult": 1, //0:简单,1:中等,2:困难
            "totalQuestSum": 2,
            "passQuestSum": 1
        },
        {
            "difficult": 2, //0:简单,1:中等,2:困难
            "totalQuestSum": 10,
            "passQuestSum": 2
        }
    ]
}
```

## 获取上传图片token
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
```
{
    "code": 0,
    "msg": "成功",
    "data": {
        "domain": "https://upload-z2.qiniup.com", //图片上传地址
        "token": "Ki7rB" //token
    }
}
```

## 上传题目
接口用途:   
接口鉴权: 否  
测试地址: https://api.baojie.ink/xmg/quest/save  
正式地址: https://api.baojie.ink/xmg/quest/save  
请求方式: POST  
请求参数:
```
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
    "gradeId": 1, //年级id
    "bookId": 1, //册id
    "unitId": 1, //该题目属于哪个单元id
    "knowledgeId": 1 //该题目属于哪个知识点id
}
```
返回结果:
```
{
    "code": 0,
    "msg": "成功",
    "data": null
}
```

## 删除题目
接口用途:   
接口鉴权: 否  
测试地址: https://api.baojie.ink/xmg/quest/delete  
正式地址: https://api.baojie.ink/xmg/quest/delete  
请求方式: GET  
请求参数:
```
id=2
```
返回结果:
```
{
    "code": 0,
    "msg": "成功",
    "data": null
}
```

## 根据id查询题目
接口用途:   
接口鉴权: 否  
测试地址: https://api.baojie.ink/xmg/quest/one  
正式地址: https://api.baojie.ink/xmg/quest/one  
请求方式: GET  
请求参数:
```
id=2
```
返回结果:
```
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
        "gradeId": 1, //年级id
        "bookId": 1, //册id
        "unitId": 1,
        "knowledgeId": 1,
        "remark": ""
    }
}
```

## 根据id修改题目
接口用途:   
接口鉴权: 否  
测试地址: https://api.baojie.ink/xmg/quest/update  
正式地址: https://api.baojie.ink/xmg/quest/update  
请求方式: POST  
请求参数:
```
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
    "gradeId": 1,
    "bookId": 1,
    "unitId": 1,
    "knowledgeId": 1
}
```
返回结果:
```
{
    "code": 0,
    "msg": "成功",
    "data": null
}
```

## 查询题目列表
接口用途:   
接口鉴权: 否  
测试地址: https://api.baojie.ink/xmg/quest/list  
正式地址: https://api.baojie.ink/xmg/quest/list  
请求方式: POST  
请求参数:
```
{
  "userId": 1, //题目上传者id
  "startTime": "", //开始时间
  "endTime": "", //结束时间
  "name": "", //题目名称,支持模糊
  "difficult": 1, //0:简单,1:中等,2:困难
  "answerType": 1, //0:选择题,1:判断题,2:填空题
  "natureType": 1, //0:基础题,1:概念题,2:综合题
  "valid": 1, //0:无效，1:审核中 , 2:审核失败 , 3:审核成功
  "gradeId": 1, //年级id
  "knowledgeId": 1 //知识点id
}
```
返回结果:
```

{
  "code": 0,
  "msg": "成功",
  "data": {
    "total": 13,
    "list": [
      {
        "questionData": {
          "img": "",
          "questionTextFirst": "2X2=()",
          "questionTextSecond": "",
          "questionTextThird": "",
          "fraction": null,
          "power": null
        },
        "id": 2,
        "answerType": 2,
        "grade": "六年级",
        "knowledge": "小数点移位",
        "reviewDes": "审核通过",
        "valid": 3,
        "commentList": [
          {
            "userName": "18585131312",
            "comment": "答案有误",
            "createTime": "2019-07-20 10:33:37"
          }
        ],
        "createTime": "2019-07-27 05:17:25"
      },
      {
        "questionData": {
          "img": "",
          "questionTextFirst": "1X2=()",
          "questionTextSecond": "",
          "questionTextThird": "",
          "fraction": null,
          "power": null
        },
        "id": 1,
        "answerType": 0,
        "grade": "六年级",
        "knowledge": "小数点移位",
        "reviewDes": "审核通过",
        "valid": 3,
        "commentList": [
          {
            "userName": "18585131312",
            "comment": "题目有问题",
            "createTime": "2019-07-06 10:18:48"
          },
          {
            "userName": "18585131312",
            "comment": "答案有误",
            "createTime": "2019-07-20 10:33:37"
          }
        ],
        "createTime": "2019-07-27 05:17:25"
      }
    ]
  }
}

```

## 审核题目
接口用途:   
接口鉴权: 是  
测试地址: https://api.baojie.ink/xmg/quest/review  
正式地址: https://api.baojie.ink/xmg/quest/review  
请求方式: POST  
请求参数:
```
{
  "id": 8, //题目id
  "reviewDes": "不过", //审核说明
  "valid": 2 //2:审核不通过 , 3:审核通过
}
```
返回结果:
```
{
    "code": 0,
    "msg": "成功",
    "data": null
}
```

# 我的财务

## 老师个人财务中心
接口用途:   
接口鉴权: 是  
测试地址: https://api.baojie.ink/xmg/finance/oneSelf  
正式地址: https://api.baojie.ink/xmg/finance/oneSelf  
请求方式: POST  
请求参数:
```
userId=1
```
返回结果:
```
{
    "code": 0,
    "msg": "成功",
    "data": {
        "uploadQuestSum": 7, //上传题目数
        "passReviewSum": 6, //通过审核题目数
        "usedSum": 3, // 被使用过题目数
        "totalMoney": null, //总赚取金额
        "withdrawAble": null, //可提现金额
        "transRecordPOList": [
        {
            "transAmount": 0.5, //提现金额
            "valid": 1, //0:转账失败 1:转账成功
            "createTime": "2019-07-07 04:47:33" //提现日期
         }
        ] //转账记录
    }
}
```

## 老师提现
接口用途: 老师提现  
接口鉴权: 是  
测试地址: https://api.baojie.ink/xmg/finance/trans2wx  
正式地址: https://api.baojie.ink/xmg/finance/trans2wx  
请求方式: POST  
请求参数:
```
{
  "userId": 1,
  "realName": "张三", //用户真实姓名
  "phone": "185815131312", //手机号
  "openId": "vdafdcadfafdz", //openId
  "amount": 100 //提现金额
}
```
返回结果:
```
{
  "code": 0,
  "msg": "成功",
  "data": null
}
```

## 添加教材
接口用途:   
接口鉴权: 是  
测试地址: https://api.baojie.ink/xmg/book/save  
正式地址: https://api.baojie.ink/xmg/book/save  
请求方式: POST  
请求参数:
```
{
  "bookName": "demoData", //名称
  "cover": "https://img.baojie.ink/a.jpg", //封面图片地址
  "bookDes": "demoData", //描述
  "gradeId": 1 //年级id
}
```
返回结果:
```
{
  "code": 0,
  "msg": "成功",
  "data": null
}
```

## 删除教材
接口用途:   
接口鉴权: 是  
测试地址: https://api.baojie.ink/xmg/book/delete?bookId=2  
正式地址: https://api.baojie.ink/xmg/book/delete?bookId=2  
请求方式: GET  
请求参数:
```

```
返回结果:
```
{
  "code": 0,
  "msg": "成功",
  "data": null
}
```

## 修改教材
接口用途:   
接口鉴权: 是  
测试地址: https://api.baojie.ink/xmg/book/update  
正式地址: https://api.baojie.ink/xmg/book/update  
请求方式: POST  
请求参数:
```
{
  "id": 2,
  "bookName": "demoData", //名称
  "cover": "https://img.baojie.ink/a.jpg", //封面图片地址
  "bookDes": "demoData", //描述
  "gradeId": 1 //年级id
}
```
返回结果:
```
{
  "code": 0,
  "msg": "成功",
  "data": null
}
```

## 修改教材封面图片
接口用途:   
接口鉴权: 是  
测试地址: https://api.baojie.ink/xmg/book/update/cover  
正式地址: https://api.baojie.ink/xmg/book/update/cover  
请求方式: POST  
请求参数:
```
{
  "id": 2,
  "cover": "https://img.baojie.ink/a.jpg" //封面图片地址
}
```
返回结果:
```
{
  "code": 0,
  "msg": "成功",
  "data": null
}
```

## 教材上架下架
接口用途:   
接口鉴权: 是  
测试地址: https://api.baojie.ink/xmg/book/valid  
正式地址: https://api.baojie.ink/xmg/book/valid  
请求方式: POST  
请求参数:
```
{
  "id": 2,
  "valid": 1 //0:下架，1：上架
}
```
返回结果:
```
{
  "code": 0,
  "msg": "成功",
  "data": null
}
```

## 根据id查询教材信息
接口用途:   
接口鉴权: 是  
测试地址: https://api.baojie.ink/xmg/book/one?bookId=2  
正式地址: https://api.baojie.ink/xmg/book/one?bookId=2  
请求方式: GET  
请求参数:
```

```
返回结果:
```
{
  "code": 0,
  "msg": "成功",
  "data": null
}
```

## 查询教材列表
接口用途:   
接口鉴权: 是  
测试地址: https://api.baojie.ink/xmg/book/list?pageIndex=1&pageSize=5  
正式地址: https://api.baojie.ink/xmg/book/list?pageIndex=1&pageSize=5  
请求方式: GET  
请求参数:
```

```
返回结果:
```
{
  "code": 0,
  "msg": "成功",
  "data": null
}
```

## 添加单元
接口用途:   
接口鉴权: 是  
测试地址: https://api.baojie.ink/xmg/unit/save  
正式地址: https://api.baojie.ink/xmg/unit/save  
请求方式: POST  
请求参数:
```
{
  "unitName": "demoData", //名称
  "unitDes": "demoData",//描述
  "bookId": 1 //教材id
}
```
返回结果:
```
{
  "code": 0,
  "msg": "成功",
  "data": null
}
```

## 删除单元
接口用途:   
接口鉴权: 是  
测试地址: https://api.baojie.ink/xmg/unit/delete?unitId=2  
正式地址: https://api.baojie.ink/xmg/unit/delete?unitId=2  
请求方式: GET  
请求参数:
```

```
返回结果:
```
{
  "code": 0,
  "msg": "成功",
  "data": null
}
```

## 修改单元
接口用途:   
接口鉴权: 是  
测试地址: https://api.baojie.ink/xmg/unit/update  
正式地址: https://api.baojie.ink/xmg/unit/update  
请求方式: POST  
请求参数:
```
{
  "id": 1,
  "unitName": "demoData",
  "unitDes": "demoData",
  "bookId": 1
}
```
返回结果:
```
{
  "code": 0,
  "msg": "成功",
  "data": null
}
```

## 根据id查询单元信息
接口用途:   
接口鉴权: 是  
测试地址: https://api.baojie.ink/xmg/unit/one?unitId=2  
正式地址: https://api.baojie.ink/xmg/unit/one?unitId=2  
请求方式: GET  
请求参数:
```

```
返回结果:
```
{
  "code": 0,
  "msg": "成功",
  "data": null
}
```

## 单元上架下架
接口用途:   
接口鉴权: 是  
测试地址: https://api.baojie.ink/xmg/unit/valid  
正式地址: https://api.baojie.ink/xmg/unit/valid  
请求方式: POST  
请求参数:
```
{
  "id": 2,
  "valid": 1 //0:下架，1：上架
}
```

## 添加知识点
接口用途:   
接口鉴权: 是  
测试地址: https://api.baojie.ink/xmg/knowledge/save  
正式地址: https://api.baojie.ink/xmg/knowledge/save  
请求方式: POST  
请求参数:
```
{
  "knowledgeName": "demoData", //知识点名称
  "knowledgeDes": "demoData", //知识点描述
  "unitId": 1, //单元id
  "simpleMax": 20, //简单题目最大数量
  "mediumMax": 20, //中等题目最大数量
  "hardMax": 10 //困难题目最大数量
}
```
返回结果:
```
{
  "code": 0,
  "msg": "成功",
  "data": null
}
```

## 删除知识点
接口用途:   
接口鉴权: 是  
测试地址: https://api.baojie.ink/xmg/knowledge/delete?knowId=2  
正式地址: https://api.baojie.ink/xmg/knowledge/delete?knowId=2  
请求方式: GET  
请求参数:
```

```
返回结果:
```
{
  "code": 0,
  "msg": "成功",
  "data": null
}
```

## 修改知识点
接口用途:   
接口鉴权: 是  
测试地址: https://api.baojie.ink/xmg/knowledge/update  
正式地址: https://api.baojie.ink/xmg/knowledge/update  
请求方式: POST  
请求参数:
```
{
  "id": 2, //知识点id
  "knowledgeName": "demoData", //知识点名称
  "knowledgeDes": "demoData", //知识点描述
  "unitId": 1, //单元id
  "simpleMax": 20, //简单题目最大数量
  "mediumMax": 20, //中等题目最大数量
  "hardMax": 10 //困难题目最大数量
}
```
返回结果:
```
{
  "code": 0,
  "msg": "成功",
  "data": null
}
```

## 根据id查询知识点信息
接口用途:   
接口鉴权: 是  
测试地址: https://api.baojie.ink/xmg/knowledge/one?knowId=2  
正式地址: https://api.baojie.ink/xmg/knowledge/one?knowId=2  
请求方式: GET  
请求参数:
```

```
返回结果:
```
{
  "code": 0,
  "msg": "成功",
  "data": {
    "id": 1,
    "knowledgeName": "小数点移位",
    "knowledgeDes": "湖南小学六年级数学上册小数乘法小数点移位",
    "unitId": 1, //单元id
    "simpleMax": 20, //简单题最大题目数量
    "passSimple": 10, //审核通过的简单题数量
    "mediumMax": 20,
    "passMedium": 6,
    "hardMax": 20,
    "passHard": 4,
    "valid": 1,
    "createTime": "2019-06-30T09:34:09",
    "updateTime": "2019-08-22T09:32:02"
  }
}
```