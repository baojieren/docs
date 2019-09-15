# 小程序接口

版本号|修改人|修改时间|修改项
:---|:---|:---|:---
1.0|任宝杰|2019-7-1|初版

## 鉴权步骤
1. 先登陆,后台使用手机号+密码方式登陆,小程序使用openId登陆
2. 登陆成功获得token
3. 以后每次请求接口在请求头携带token标识
4. 请求头token格式: Authorization: Bearer token   //Bearer为固定标识，空格后接token串

## 登陆注册

>### 小程序获取openId

接口用途:   
接口鉴权: 否  
测试地址: https://api.baojie.ink/xmg/openId/mini  
正式地址: https://api.baojie.ink/xmg/openId/mini  
请求方式: GET  
请求参数:
```
code="asdfg"
```
返回结果:
```json
{
  "code": 0,
  "msg": "成功",
  "data": null
}
```

>### 小程序登陆

接口用途:   
接口鉴权: 否  
测试地址: https://api.baojie.ink/xmg/login/mini  
正式地址: https://api.baojie.ink/xmg/login/mini  
请求方式: POST  
请求参数:
```json
{
  "openId": "qweqwe"
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

## 发现页

>### 模糊搜索教材

接口用途:   
接口鉴权: 是  
测试地址: https://api.baojie.ink/xmg/mini/search/book  
正式地址: https://api.baojie.ink/xmg/mini/search/book  
请求方式: GET  
请求参数:
```
bookName="六年级数学"
```
返回结果:
```json
{
  "code": 0,
  "msg": "成功",
  "data": [
    {
      "id": 1,
      "cover": "",
      "bookName": "六年级数学上册",
      "bookDes": "湖南小学六年级数学上册",
      "gradeId": 6,
      "valid": 1,
      "createTime": "2019-06-30 09:32:56",
      "updateTime": "2019-06-30 11:15:40"
    }
  ]
}
```

>### 查询最后一次答题记录

接口用途:   
接口鉴权: 是  
测试地址: https://api.baojie.ink/xmg/mini/lastRecord  
正式地址: https://api.baojie.ink/xmg/mini/lastRecord  
请求方式: POST  
请求参数:
```json
{
  "userId": 1, //答题人id
  "unitId": 1, //单元id
  "knowledgeId": 1, //知识点id（0表示综合练习）
  "mode": 1 //0:随机练习,1:针对练习
}
```
返回结果:
```json
{
  "code": 0,
  "msg": "成功",
  "data": {
    "unitId": 1, //单元ID
    "unitName": "整数乘法", //单元名称
    "knowledgeId": 1, //知识点ID
    "knowledgeName": "整数乘法", //知识点名称
    "model": 1, //0:随机练习,1:针对性练习
    "level": "D", //得分等级
    "suggest": "赶紧报补习班", //建议
    "rightAndWrongList": [ //做题对错情况
      {
        "natureType": 0, //0:基础题目,1:概念题,2:综合题
        "rightSum": 0, //答对数量
        "wrongSum": 1 //答错数量
      },
      {
        "natureType": 1,
        "rightSum": 0,
        "wrongSum": 1
      },
      {
        "natureType": 2,
        "rightSum": 0,
        "wrongSum": 1
      }
    ],
    "wrongKnowledgeList": [ //做错的知识点情况
      {
        "knowledgeId": 1, //知识点ID
        "knowledgeName": "整数乘法", //知识点名称
        "natureType": 1 //0:基础题目,1:概念题,2:综合题
      },
      {
        "knowledgeId": 1,
        "knowledgeName": "整数乘法",
        "natureType": 0
      },
      {
        "knowledgeId": 3,
        "knowledgeName": "小数点",
        "natureType": 2
      }
    ]
  }
}
```

>### 上次练习错题

接口用途:   
接口鉴权: 是  
测试地址: https://api.baojie.ink/xmg/mini/allWrong  
正式地址: https://api.baojie.ink/xmg/mini/allWrong  
请求方式: GET  
请求参数:
```
recordId=1 //答题记录id
```
返回结果:
```json
{
  "code": 0,
  "msg": "成功",
  "data": [
    {
      "questId": 1,
      "recordId": 1,
      "name": "2+2=4?",
      "analysis": "正确答案是4啊",
      "answerType": 1,
      "questKey": "对",
      "studentKey": "错"
    },
    {
      "questId": 2,
      "recordId": 1,
      "name": "4+2等于()",
      "analysis": "正确答案是6啊",
      "answerType": 2,
      "questKey": "6",
      "studentKey": "B"
    },
    {
      "questId": 3,
      "recordId": 1,
      "name": "0.5小数点右移动2位相当于扩大多少倍?",
      "analysis": "右移一位是10倍,2位是100倍",
      "answerType": 0,
      "questKey": "A",
      "studentKey": "C"
    }
  ]
}
```

>### 上次练习知识点错题情况

接口用途:   
接口鉴权: 是  
测试地址: https://api.baojie.ink/xmg/mini/knowledgeWrong  
正式地址: https://api.baojie.ink/xmg/mini/knowledgeWrong  
请求方式: GET  
请求参数:
```
recordId=1&knowledgeId=1&natureType=1
```
返回结果:
```json
{
  "code": 0,
  "msg": "成功",
  "data": [
    {
      "questId": 2, //题目id
      "recordId": 1, //答题记录id
      "name": "4+2等于()", //题干
      "analysis": "正确答案是6啊", //题目解析
      "answerType": 2, //0:基础题,1:概念题,2:综合题
      "questKey": "6", //题目答案
      "studentKey": "B" //学生答案
    }
  ]
}
```

>### 生成强化训练练习

接口用途: 生成强化训练练习  
接口鉴权: 是  
测试地址: https://api.baojie.ink/xmg/mini/wrongTrain?recordId=1&lastWrongRecordId=2&knowledgeId=2&natureType=3  
正式地址: https://api.baojie.ink/xmg/mini/wrongTrain?recordId=1&lastWrongRecordId=2&knowledgeId=2&natureType=3  
请求方式: GET  
请求参数:
```
recordId=1 // 答题记录id
lastWrongRecordId=2 // 最后一次强化训练答题记录id，如果第一次生成错题强化训练，可以不传
knowledgeId=2 // 知识点错题练习时传
natureType=3 // 知识点错题练习时传
```
返回结果:
```json
{
  "recordId": 1, //答题记录id
  "wrongRecordId": 12, //本次生成错题强化训练练习id
  "questList": [] // 题目列表
}
```

>### 提交错题强化训练

接口用途: 提交错题强化训练  
接口鉴权: 是  
测试地址: https://api.baojie.ink/xmg/mini/submitWrong  
正式地址: https://api.baojie.ink/xmg/mini/submitWrong  
请求方式: POST  
请求参数:
```json
{
  "lastWrongRecordId": 42,
  "questList": [
    {
      "key": "6",
      "questId": 43
    },
    {
      "key": "C",
      "questId": 45
    },
    {
      "key": "1",
      "questId": 49
    },
    {
      "key": "B",
      "questId": 50
    },
    {
      "key": "1",
      "questId": 54
    },
    {
      "key": "B",
      "questId": 59
    },
    {
      "key": "A",
      "questId": 61
    }
  ]
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

>### 用户点击有话说

接口用途:   
接口鉴权: 是  
测试地址: https://api.baojie.ink/xmg/mini/wyhs  
正式地址: https://api.baojie.ink/xmg/mini/wyhs  
请求方式: GET  
请求参数:
```
questId=1 //题目id
```
返回结果:
```json
{
  "code": 0,
  "msg": "成功",
  "data": {
    "commentPOList": { //给用户预留的评论语句
      "0": [ //题干的评论语句
        {
          "id": 1,
          "forType": 0,
          "comment": "题目有问题"
        },
        {
          "id": 2,
          "forType": 0,
          "comment": "题目不错"
        }
      ],
      "1": [ //解析的评论语句
        {
          "id": 3,
          "forType": 1,
          "comment": "解析有误"
        },
        {
          "id": 4,
          "forType": 1,
          "comment": "解析不错"
        }
      ],
      "2": [ //答案的评论语句
        {
          "id": 5,
          "forType": 2,
          "comment": "答案有误"
        }
      ]
    },
    "userCommentList": [ //该题目的其他人的评论
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
    ]
  }
}
```

>### 用户提交评论

接口用途:   
接口鉴权: 是  
测试地址: https://api.baojie.ink/xmg/mini/comment  
正式地址: https://api.baojie.ink/xmg/mini/comment  
请求方式: POST  
请求参数:
```json
{
  "list": [
    {
      "questId": 1, //题目id
      "userId": 1, //用户id
      "commentId": 5 //评论语句id
    },
    {
      "questId": 2,
      "userId": 1,
      "commentId": 5
    }
  ]
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

>### 检查用户是否有资格生成针对训练和强化训练

接口用途:   
接口鉴权: 是  
测试地址: https://api.baojie.ink/xmg/mini/train/check/permission?userId=182?userId=182  
正式地址: https://api.baojie.ink/xmg/mini/train/check/permission?userId=182?userId=182  
请求方式: GET  
请求参数:
```
userId=182 // 用户id
```
返回结果:
```json
{
  "code": 0,
  "msg": "成功",
  "data": true // true: 有资格 false： 没资格，请充值
}
```
>### 生成随机练习

接口用途:   
接口鉴权: 是  
测试地址: https://api.baojie.ink/xmg/mini/train/random  
正式地址: https://api.baojie.ink/xmg/mini/train/random  
请求方式: PSOT  
请求参数:
```json
{
  "userId": 1, //答题人id
  "unitId": 1, //单元id
  "knowledgeId": 1 //知识点id 0:综合练习
}
```
返回结果:
```json
{
  "code": 0,
  "msg": "成功",
  "data": [
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
      "limitTime": 10,
      "answerType": 0,
      "optionList": [
        {
          "key": "A",
          "value": "1"
        },
        {
          "key": "B",
          "value": "10"
        },
        {
          "key": "C",
          "value": "100"
        },
        {
          "key": "D",
          "value": "2"
        }
      ]
    },
    {
      "questionData": {
        "img": "",
        "questionTextFirst": "(1+3)X2=()",
        "questionTextSecond": "",
        "questionTextThird": "",
        "fraction": null,
        "power": null
      },
      "id": 12,
      "limitTime": 10,
      "answerType": 2,
      "optionList": null
    }
  ]
}
```

>### 生成针对练习

接口用途:   
接口鉴权:   
测试地址: https://api.baojie.ink/xmg/mini/train/pro  
正式地址: https://api.baojie.ink/xmg/mini/train/pro  
请求方式: POST  
请求参数:
```json
{
  "userId": 1, //用户id
  "unitId": 1, //单元id
  "knowledgeId": 0 //知识点id ,0:综合练习
}
```
返回结果:
```json
{
  "code": 0,
  "msg": "成功",
  "data": [
    {
      "questionData": {
        "img": "",
        "questionTextFirst": "100/130=()",
        "questionTextSecond": "",
        "questionTextThird": "",
        "fraction": null,
        "power": null
      },
      "id": 35,
      "limitTime": 10,
      "answerType": 2,
      "optionList": null
    }
  ]
}
```

>### 交卷

接口用途:   
接口鉴权: 是  
测试地址: https://api.baojie.ink/xmg/mini/train/submit  
正式地址: https://api.baojie.ink/xmg/mini/train/submit  
请求方式: POST  
请求参数:
```json
{
  "recordId": 6, //答题记录id
  "questList": [
    {
      "questId": 5, //题目id
      "key": "101" //学生填写的答案
    },{
      "questId": 35,
      "key": "-3"
    }
  ]
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

>### 用户开通会员（支付下单）

接口用途:   
接口鉴权: 是  
测试地址: https://api.baojie.ink/xmg/order/pre  
正式地址: https://api.baojie.ink/xmg/order/pre  
请求方式: POST  
请求参数:
```json
{
  "userId": 1,
  "openId": "asdfrqerew",
  "goodsId": 1// 0：包月，1：半年
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

>### 查询错题强化训练错题列表

接口用途: 查询错题强化训练错题列表  
接口鉴权: 是  
测试地址: https://api.baojie.ink/xmg/mini/wrongTrainResult?wrongRecordId=42  
正式地址: https://api.baojie.ink/xmg/mini/wrongTrainResult?wrongRecordId=42  
请求方式: GET  
请求参数:
```
wrongRecordId=42 // 错题强化训练记录id
```
返回结果:
```json
{
  "code": 0,
  "msg": "成功",
  "data": [
    {
      "questionData": {
        "img": "",
        "questionTextFirst": "文本1",
        "questionTextSecond": "文本2",
        "questionTextThird": "文本3",
        "fraction": [
          {
            "fenzi": "5",
            "fenmu": "6",
            "integral": "1",
            "symbol": "中文"
          },
          {
            "fenzi": "1",
            "fenmu": "2",
            "integral": "文本",
            "symbol": "测试"
          },
          {
            "fenzi": "4",
            "fenmu": "15",
            "integral": "2",
            "symbol": "测试"
          }
        ],
        "power": [
          {
            "baseNumber": "",
            "supNumber": "",
            "symbol": ""
          }
        ]
      },
      "questId": 46,
      "recordId": 42,
      "analysis": {
        "questionTextFirst": null,
        "questionTextSecond": null,
        "fraction": null,
        "power": null
      },
      "answerType": 1,
      "natureType": 1,
      "knowledgeId": 1,
      "questKey": "对",
      "studentKey": "错"
    }
  ]
}
```