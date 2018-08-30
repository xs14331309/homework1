## 乔布阅读B平台考试后台管理系统接口文档 ##

[TOC]
### 试卷管理
#### 1.试卷保存

- **请求URL**
> [exam/paper/save](#)

- **请求方式** 
>**POST**

- **请求参数**
>| 请求参数      |     参数类型 |   参数说明   | 参数需要
| :-------- | :--------| :------ |:------
| id|  Long| 试卷id|**新建**试卷optional，**更新**试卷requried|
| departmentId| String| 企业id| requried|
| name | String | 试卷名称| requried|
| time | Integer | 试卷时长| requried|
| totalScore | Float| 满分| requried|
| passScore | Float| 及格分| requried|
| isOptionOutoforder | String| 选项是否乱序| requried|
| refBookId | String| 参考书id，多个以'&#124;'分割| optional|
| checkFlg | String | 是否允许查看错题| requried |

- **返回参数**
> | 返回参数      |     参数类型 |   参数说明   |
| :-------- | :--------| :------ |
| msg|   boolean|  请求成功与否|
| code|   Integer|  执行结果code|

- **返回示例**
>   
**```success```**
{
  "msg": "success",
  "code": 200
}
>
**```failed```**
{
  "msg": "添加试卷名称已存在",
  "code": 400
}

#### 2.单个试卷查询

- **请求URL**
> [exam/paper/query/{paperId}](#)

- **请求方式** 
>**GET**

- **请求参数**
>| 请求参数      |     参数类型 |   参数说明   | 参数需要
| :-------- | :--------| :------ |:------
| paperId|  Long| 试卷id| requried|

- **返回参数**
> | 返回参数      |     参数类型 |   参数说明   |
| :-------- | :--------| :------ |
| msg|   boolean|  请求成功与否 |
| code|   Integer|  执行结果code |
|paper | Paper Model | 试卷详情 |
| books | Book Model | 参考书列表 |

- **返回示例**
>   
**```success```**
{
   "msg": "success",
   "code": 200,
   "books": [
      {
         "bookId": 307431,
         "author": "文",
         "bookName": "工作分析法",
         "bookType": 2,
         "departmentId": null,
         "bookSource": 1,
         "sourceBookId": "99401",
         "sourceBookClassify": "10857",
         "bookClassifyId": 62,
         "filePath": null,
         "fileType": null,
         "isbn": "",
         "largeLogo": null,
         "logo": null,
         "pass": true,
         "sourcePass": true,
         "publisher": null,
         "readPath": null,
         "rebate": null,
         "remark": null,
         "isBuy": null,
         "isCanBuy": true,
         "isCanFreeGet": null,
         "edition": "1",
         "adWords": null,
         "isFluentRead": true,
         "isFree": false,
         "authorInfo": null,
         "info": null,
         "jdPrice": null,
         "language": null,
         "catalog": null,
         "orgJdPrice": null,
         "price": null,
         "priceMessage": null,
         "publishTime": null,
         "wordCount": null,
         "star": 0,
         "editorPick": null,
         "paperBookId": "99401",
         "promotion": null,
         "analyzeStatus": 0,
         "createTime": "2018-08-25 16:50:16",
         "label": null,
         "bookuri": "99401",
         "sourceOtherBookClassifyIds": null,
         "bookstore": "default",
         "ebook": true
      }
   ],
   "paper": {
      "id": 1,
      "departmentId": "02eb40b714534f5c86ba246779af4bda",
      "name": "人力资源",
      "time": 120,
      "totalScore": 100,
      "passScore": 60,
      "isOptionOutoforder": "Y",
      "refBookId": "307431,40559",
      "checkFlg": "Y"
   }
}
>
**```failed```**
{
  "msg": "试卷不存在",
  "code": 400
}

#### 3.试卷删除

- **请求URL**
> [exam/paper/delete](#)

- **请求方式** 
>**POST**

- **请求参数**
> | 请求参数      |     参数类型 |   参数说明   | 参数需要
| :-------- | :--------| :------ |:------
| paperId|  Long| 试卷id| required|

- **返回参数**
> | 返回参数      |     参数类型 |   参数说明   |
| :-------- | :--------| :------ |
| msg|   boolean|  请求成功与否|
| code|   Integer|  执行结果code|

- **返回示例**
>   
**```success```**
{
  "msg": "success",
  "code": 200
}
>
**```failed```**
{
  "msg": "有考试:人力资源使用该试卷，无法删除",
  "code": 400
}

#### 4.企业试卷列表

- **请求URL**
> [exam/paper/deptPapers](#)

- **请求方式** 
>**GET**

- **请求参数**
>| 请求参数      |     参数类型 |   参数说明   | 参数需要
| :-------- | :--------| :------ |:------
| departmetnId|  String| 企业id| requried|
| pageNo| Long| 页码| required|
| pageSize| Long| 页大小| required|

- **返回参数**
> | 返回参数      |     参数类型 |   参数说明   |
| :-------- | :--------| :------ |
| msg|   boolean|  请求成功与否|
| code|   Integer|  执行结果code|

- **返回示例**
>   
**```success```**
{
   "msg": "success",
   "code": 200,
   "paperList": [
      {
         "id": 1,
         "departmentId": "02eb40b714534f5c86ba246779af4bda",
         "name": "人力资源",
         "time": 120,
         "totalScore": 100,
         "passScore": 60,
         "isOptionOutoforder": "Y",
         "refBookId": "307431,40559",
         "checkFlg": "Y"
      }
   ]
}
>
**```failed```**
{
  "msg": "参数错误",
  "code": 400
}

### 试卷题库管理
#### 1.题目编辑后新增（试卷题库/题库）|手工录入试题

- **请求URL**
> [exam/examQuestion/insert](#)

- **请求方式** 
>**POST**

- **请求参数**
>| 请求参数      |     参数类型 |   参数说明   | 参数需要
| :-------- | :--------| :------ |:------
| id| Long| 试题id|**新建**试题optional，**更新**试卷requried|
| departmentId| String| 企业id| required|
| type| String| 试题类型，**1-单选，2-多选，3-判断**| required|
| source| String| 试题来源，**AF-人工，AI-判断**| required|
| answer| String| 试题答案| required|
| content| String| 试题题干| required|
| pointId| String| 参考书知识点| required|
| createTime| Date| 试题创建时间| optional|
| remark| String| 试题备注| optional|
| labels| String| 试题标签id，多个以'&#124;'分割| optional|
| labelNames| String| 试题标签名称，多个以'&#124;'分割| optional|
| options| String| 试题选项，多个以'&#124;'分割| **type=1，2**时required，其他情况Unwanted|
| paperId| String| 试卷id | required |

- **返回参数**
> | 返回参数      |     参数类型 |   参数说明   |
| :-------- | :--------| :------ |
| msg|   boolean|  请求成功与否|
| code|   Integer|  执行结果code|

- **返回示例**
>   
**```success```** 
'''多次重复添加，依然显示成功'''
{
  "msg": "success",
  "code": 200
}
>
**```failed```**
'''缺少参数'''
{
  "timestamp": "2018-08-28 15:14:27",
  "status": 500,
  "error": "Internal Server Error",
  "exception": "com.jobreading.common.exception.JrException",
  "message": "缺少必要参数信息",
  "path": "/examQuestion/insert"
}
>
'''试题重复'''
{
  "msg": "更新失败：题库中存在相同题目，您可以在题库中搜索添加到试卷题库。",
  "code": 500
}

#### 2.试卷题库试题查看

- **请求URL**
> [exam/examQuestion/list](#)

- **请求方式** 
>**GET**

- **请求参数**
>| 请求参数      |     参数类型 |   参数说明   | 参数需要
| :-------- | :--------| :------ |:------
| paperId|  Long| 试卷id| required|
| pageNo| Long| 页码| required|
| pageSize| Long| 页大小| required|

- **返回参数**
> | 返回参数      |     参数类型 |   参数说明   |
| :-------- | :--------| :------ |
| msg|   boolean|  请求成功与否|
| code|   Integer|  执行结果code|

- **返回示例**
>   
**```success```**
{
   "msg": "success",
   "code": 200,
   "questionList": [
      {
         "id": 21,
         "departmentId": "02eb40b714534f5c86ba246779af4bda",
         "type": "1",
         "source": "AF",
         "answer": "0|1|0|0",
         "content": "人力资源大数据的价值主要体现在有效运用大数据思维与技术",
         "pointId": null,
         "createTime": "2018-08-28 10:10:49",
         "remark": null,
         "labels": "51|50",
         "labelNames": "工业|数学",
         "options": "绩效管理|薪酬与激励体系|员工福利|建模分析"
      },
      {
         "id": 22,
         "departmentId": "02eb40b714534f5c86ba246779af4bda",
         "type": "1",
         "source": "AF",
         "answer": "0|0|1|0",
         "content": "人力资源大数据的价值主要体现在有效运用大数据思维与技术",
         "pointId": null,
         "createTime": "2018-08-28 09:29:13",
         "remark": null,
         "labels": "51",
         "labelNames": "工业",
         "options": "绩效管理|薪酬与激励体系|员工福利|建模分析"
      }
   ]
}
>
**```failed```**
{
  "msg": "参数错误",
  "code": 500
}

#### 3. 试卷题库搜索

- **请求URL**
> [exam/examQuestion/search](#)

- **请求方式** 
>**GET**

- **请求参数**
>| 请求参数      |     参数类型 |   参数说明   | 参数需要
| :-------- | :--------| :------ |:------
| paperId|  Long| 试卷id| required|
| content| String| 试题内容| optional|
| source| String| 试题来源，**AF-人工，AI-判断**| optional|
| pageNo| Long| 页码| required|
| pageSize| Long| 页大小| required|

- **返回参数**
> | 返回参数      |     参数类型 |   参数说明   |
| :-------- | :--------| :------ |
| msg|   boolean|  请求成功与否|
| code|   Integer|  执行结果code|

- **返回示例**
>   
**```success```**
{
   "msg": "success",
   "code": 200,
   "questionList": [
      {
         "id": 21,
         "departmentId": "02eb40b714534f5c86ba246779af4bda",
         "type": "1",
         "source": "AF",
         "answer": "0|1|0|0",
         "content": "人力资源大数据的价值主要体现在有效运用大数据思维与技术",
         "pointId": null,
         "createTime": "2018-08-28 10:10:49",
         "remark": null,
         "labels": "51|50",
         "labelNames": "工业|数学",
         "options": "绩效管理|薪酬与激励体系|员工福利|建模分析"
      }
   ]
}
**```failed```**
{
  "msg": "查询参数必须包含paperId",
  "code": 400
}

#### 4. 试卷题库删除

- **请求URL**
> [exam/examQuestion/delete](#)

- **请求方式** 
>**POST**

- **请求参数**
>| 请求参数      |     参数类型 |   参数说明   | 参数需要
| :-------- | :--------| :------ |:------
| paperId|  Long| 试卷id| required|
| questionIds| Array[Long]| 试题id列表| required|

- **返回参数**
> | 返回参数      |     参数类型 |   参数说明   |
| :-------- | :--------| :------ |
| msg|   boolean|  请求成功与否|
| code|   Integer|  执行结果code|

- **返回示例**
>   
**```success```**
{
  "msg": "success",
  "code": 200
}

#### 5. 从题库中导入试题

- **请求URL**
> [exam/examQuestion/addIntoPaper](#)

- **请求方式** 
>**POST**

- **请求参数**
>| 请求参数      |     参数类型 |   参数说明   | 参数需要
| :-------- | :--------| :------ |:------
| paperId|  Long| 试卷id| required|
| questionIds| Array[Long]| 试题id列表| required|

- **返回参数**
> | 返回参数      |     参数类型 |   参数说明   |
| :-------- | :--------| :------ |
| msg|   boolean|  请求成功与否|
| code|   Integer|  执行结果code|

- **返回示例**
> 
**```success```**
 '''重复添加无效，但依然显示成功'''
{
  "msg": "success",
  "code": 200
}

#### 6. 批量导入获取下载模板

- **请求URL**
> [exam/examQuestion/fileDownLoad](#)

- **请求方式** 
>**GET**

- **请求参数**
>| 请求参数      |     参数类型 |   参数说明   | 参数需要
| :-------- | :--------| :------ |:------


- **返回参数**
> | 返回参数      |     参数类型 |   参数说明   |
| :-------- | :--------| :------ |
| msg|   boolean|  请求成功与否|
| code|   Integer|  执行结果code|

#### 7. 批量导入上传文件

- **请求URL**
> [exam/examQuestion/fileUpload](#)

- **请求方式** 
>**POST**

- **请求参数**
>| 请求参数      |     参数类型 |   参数说明   | 参数需要
| :-------- | :--------| :------ |:------
| file|  File| 试题文件| required|
| paperId| Long| 试卷id，若缺失则只上传入总题库| optional|
| departmentId| String| 企业id| required|

- **返回参数**
> | 返回参数      |     参数类型 |   参数说明   |
| :-------- | :--------| :------ |
| msg|   boolean|  请求成功与否|
| code|   Integer|  执行结果code|

- **返回示例**
>   
**```success```**
{
  "msg": "success",
  "code": 200
}
**```failed```**
'''文件不是excel文件'''
{
  "timestamp": "2018-08-28 15:58:27",
  "status": 500,
  "error": "Internal Server Error",
  "exception": "com.jobreading.common.exception.JrException",
  "message": "上传文件格式不正确",
  "path": "/examQuestion/fileUpload"
}
'''试题格式不正确'''
to do


### 考场管理
#### 1. 新建考场

- **请求URL**
> [exam/exam/create](#)

- **请求方式** 
>**POST**

- **请求参数**
>| 请求参数      |     参数类型 |   参数说明   | 参数需要
| :-------- | :--------| :------ |:------
| paperId| Long| 试卷id| required|
| departmentId| String| 企业id| required|
| name| String| 考场名称| required|
| beginTime| Date| 考试系统开启时间| required|
| endTime| Date| 考试系统关闭时间| required|
| createTime| Date| 考试创建时间| optional|
| boundTime| Integer| 开考进场截止时间，以分钟计| required|
| examType| String |考试类型 **C-集中考试，R-随来随考**| required|
| initiator| String| 发起人|required|
| remark| String| 备注| optional|
| reportStatus| String| 考试报告状态 **N-未生成报告 ，Y-已生成报告**| optional|
| status| String| 考试当前状态 **U-预计状态 P-考试中 D-考试结束**| optional|

- **返回参数**
> | 返回参数      |     参数类型 |   参数说明   |
| :-------- | :--------| :------ |
| msg|   boolean|  请求成功与否|
| code|   Integer|  执行结果code|

- **返回示例**
>
**```success```**
{
  "msg": "success",
  "code": 200
}
**```failed```**
'''名字相同'''
{
  "msg": "已经有相同名字的考试存在",
  "code": 400
}
'''boundTime字段错误'''
{
  "msg": "截止时间不能大于结束时间",
  "code": 400
}


#### 2. 获取考场详情

- **请求URL**
> [/exam/query/{examId}](#)

- **请求方式** 
>**POST**

- **请求参数**
>| 请求参数      |     参数类型 |   参数说明   | 参数需要
| :-------- | :--------| :------ |:------
| examId|  Long| 考场id| required|

- **返回参数**
> | 返回参数      |     参数类型 |   参数说明   |
| :-------- | :--------| :------ |
| msg|   boolean|  请求成功与否|
| code|   Integer|  执行结果code|
| exam|  Model| 考场详情| 

- **返回示例**
> 
**```success```**
{
  "msg": "success",
  "exam": {
    "eid": 1,
    "pname": "人力资源",
    "departmentId": "02eb40b714534f5c86ba246779af4bda",
    "boundTime": 30,
    "initiator": "工会",
    "length": 120,
    "examType": "R",
    "reportStatus": "U",
    "remark": "华北区使用",
    "pid": 1,
    "ename": "人力资源",
    "createTime": "2018-08-26 07:21:08",
    "beginTime": "2018-08-27 10:00:00",
    "endTime": "1970-01-19 02:29:02",
    "status": "D"
  },
  "code": 200
}

#### 3. 考场更新

- **请求URL**
> [/exam/update](#)

- **请求方式** 
>**GET**

- **请求参数**
>| 请求参数      |     参数类型 |   参数说明   | 参数需要
| :-------- | :--------| :------ |:------
|id| Long| 考场id| required|
| name| String| 考场名称| required|
| paperId| Long| 试卷id| required|
| departmentId| String| 企业id| required|
| beginTime| Date| 考试系统开启时间| required|
| endTime| Date| 考试系统关闭时间| required|
| createTime| Date| 考试创建时间| optional|
| boundTime| Integer| 开考进场截止时间，以分钟计| required|
| examType| String |考试类型 **C-集中考试，R-随来随考**| required|
| initiator| String| 发起人|required|
| remark| String| 备注| optional|
| reportStatus| String| 考试报告状态 **N-未生成报告 ，Y-已生成报告**| optional|
| status| String| 考试当前状态 **U-预计状态 P-考试中 D-考试结束**| optional|

- **返回参数**
> | 返回参数      |     参数类型 |   参数说明   |
| :-------- | :--------| :------ |
| msg|   boolean|  请求成功与否|
| code|   Integer|  执行结果code|

- **返回示例**
> 
**```success```**
{
  "msg": "success",
  "code": 200
}

**```failed```**
'''考场内含有考生不能更新'''
{
  "msg": "考场内含有考生，请先到管理考生页面删除考生",
  "code": 400
}

#### 4. 考场删除

- **请求URL**
> [/exam/delete](#)

- **请求方式** 
>**POST**

- **请求参数**
>| 请求参数      |     参数类型 |   参数说明   | 参数需要
| :-------- | :--------| :------ |:------
| examId|  Long| 考场id| required|

- **返回参数**
> | 返回参数      |     参数类型 |   参数说明   |
| :-------- | :--------| :------ |
| msg|   boolean|  请求成功与否|
| code|   Integer|  执行结果code|

- **返回示例**
> 
**```success```**
{
  "msg": "success",
  "code": 200
}
**```failed```**
'''考场内含有考生不能删除'''
{
  "msg": "考场内含有考生，请先到管理考生页面删除考生",
  "code": 400
}

#### 5. 搜索企业所有考试

- **请求URL**
> [/exam/list/{departmentId}](#)

- **请求方式** 
>**GET**

- **请求参数**
>| 请求参数      |     参数类型 |   参数说明   | 参数需要
| :-------- | :--------| :------ |:------
| departmentId|  String| 企业id| required|
| name|  String| 考试名称| optional|
| status|  String| 考试状态 **U-待考，P-正在考试，D-已结束**| optional|

- **返回参数**
> | 返回参数      |     参数类型 |   参数说明   |
| :-------- | :--------| :------ |
| msg|   boolean|  请求成功与否|
| code|   Integer|  执行结果code|
| exams|  Array[Model]| 考场列表详情| 

- **返回示例**
> 
**```success```**
{
  "msg": "success",
  "code": 200,
  "exams": [
    {
      "eid": 1,
      "pname": "人力资源",
      "departmentId": "02eb40b714534f5c86ba246779af4bda",
      "boundTime": 30,
      "initiator": "工会",
      "length": 120,
      "count": 11,
      "examType": "R",
      "reportStatus": "U",
      "remark": "华北区使用",
      "pid": 1,
      "ename": "人力资源",
      "createTime": "2018-08-26 07:21:08",
      "beginTime": "2018-08-27 10:00:00",
      "endTime": "1970-01-19 02:29:02",
      "status": "D"
    }
  ]
}

#### 6. 考场试卷或考场某考生试卷查询

- **请求URL**
> [/exam/query/using](#)

- **请求方式** 
>**GET**

- **请求参数**
>| 请求参数      |     参数类型 |   参数说明   | 参数需要
| :-------- | :--------| :------ |:------
| examId|  Long| 考场id| required|
| employeeId| String| 考生id **null-监考调用，not null-用户报告使用**| optional

- **返回参数**
> | 返回参数      |     参数类型 |   参数说明   |
| :-------- | :--------| :------ |
| msg|   boolean|  请求成功与否|
| code|   Integer|  执行结果code|
| questions| Array[Model]| 试题列表|

- **返回示例**
> 
**```success```**
{
  "msg": "success",
  "code": 200,
  "questions": [
    {
      "id": 4,
      "departmentId": "02eb40b714534f5c86ba246779af4bda",
      "type": "1",
      "source": "AI",
      "answer": "0|0|0|1",
      "content": "有了绩效考核就能保证实现______吗？",
      "pointId": "99403.0.0.0-0.7",
      "createTime": "2018-08-26 10:57:32",
      "remark": null,
      "labels": null,
      "labelNames": null,
      "options": "教育目标|组织管理|业绩目标|组织目标"
    },
    {
      "id": 16,
      "departmentId": "02eb40b714534f5c86ba246779af4bda",
      "type": "1",
      "source": "AI",
      "answer": "0|0|1|0",
      "content": "从社会学的角度上看，绩效意味着每一个______按照社会分工所确定的角色承担他的那一份职责。",
      "pointId": "99403.0.0.0.0.2-0.0",
      "createTime": "2018-08-27 15:53:32",
      "remark": null,
      "labels": null,
      "labelNames": null,
      "options": "社会竞争|社会弱势群体|社会成员|社会适应性"
    }
  ]
}



### 考场考生管理
#### 1. 通过id添加考生

- **请求URL**
> [/examEmployee/addEmployeeByEid](#)

- **请求方式** 
>**POST**

- **请求参数**
>| 请求参数      |     参数类型 |   参数说明   | 参数需要
| :-------- | :--------| :------ |:------
| examId|  Long| 考场id| required|
| employeeIds| Array[String]| 考生id列表| required|

- **返回参数**
> | 返回参数      |     参数类型 |   参数说明   |
| :-------- | :--------| :------ |
| msg|   boolean|  请求成功与否|
| code|   Integer|  执行结果code|

- **返回示例**
> 
**```success```**
{
  "msg": "success",
  "code": 200
}
**```failed```**
'''考场或者考生id不存在'''
{
  "timestamp": "2018-08-29 15:19:39",
  "status": 500,
  "error": "Internal Server Error",
  "exception": "org.springframework.dao.DataIntegrityViolationException",
  "message": "\r\n### Error updating database.",
  "path": "/examEmployee/addEmployeeByEid"
}

#### 2. 通过用户组添加考生

- **请求URL**
> [/examEmployee/addEmployeeByRole](#)

- **请求方式** 
>**POST**

- **请求参数**
>| 请求参数      |     参数类型 |   参数说明   | 参数需要
| :-------- | :--------| :------ |:------
| examId|  Long| 考场id| required|
| roleIds| Array[string]| 用户组id| required|
| departmentId| String| 企业id| required|

- **返回参数**
> | 返回参数      |     参数类型 |   参数说明   |
| :-------- | :--------| :------ |
| msg|   boolean|  请求成功与否|
| code|   Integer|  执行结果code|

- **返回示例**
> 
**```success```**
{
  "msg": "success",
  "code": 200,
}

#### 3. 移除考生

- **请求URL**
> [/examEmployee/deleteEmployee](#)

- **请求方式** 
>**POST**

- **请求参数**
>| 请求参数      |     参数类型 |   参数说明   | 参数需要
| :-------- | :--------| :------ |:------
| examId|  Long| 考场id| required|
| employeeIds| Array[String]| 考生id列表 **null-删除全部考生，not null-删除id指定考生**| optional|

- **返回参数**
> | 返回参数      |     参数类型 |   参数说明   |
| :-------- | :--------| :------ |
| msg|   boolean|  请求成功与否|
| code|   Integer|  执行结果code|

- **返回示例**
> 
**```success```**
{
  "msg": "success",
  "code": 200
}

#### 4. 查询企业用户组及人数

- **请求URL**
> [/examEmployee/listRole](#)

- **请求方式** 
>**GET**

- **请求参数**
>| 请求参数      |     参数类型 |   参数说明   | 参数需要
| :-------- | :--------| :------ |:------
| departmentId|  String| 企业id| required|
| status| Long| 删除状态 **default:1**| optional|

- **返回参数**
> | 返回参数      |     参数类型 |   参数说明   |
| :-------- | :--------| :------ |
| msg|   boolean|  请求成功与否|
| code|   Integer|  执行结果code|
| roleAndCount| Array[Model]| 用户组id、名称、数目|

- **返回示例**
> 
{
  "msg": "success",
  "code": 200,
  "roleAndCount": [
    {
      "role_name": "开发组",
      "count": 11,
      "id": "1c28280eac5543a58b252d8e71cb6f51"
    }
  ]
}

#### 5. 查询考场某考生详情

- **请求URL**
> [/examEmployee/querySingle](#)

- **请求方式** 
>**GET**

- **请求参数**
>| 请求参数      |     参数类型 |   参数说明   | 参数需要
| :-------- | :--------| :------ |:------
| departmentId|  String| 企业id| required|
| status| Long| 删除状态 **default:1**| optional|

- **返回参数**
> | 返回参数      |     参数类型 |   参数说明   |
| :-------- | :--------| :------ |
| msg|   boolean|  请求成功与否|
| code|   Integer|  执行结果code|
| roleAndCount| Array[Model]| 用户组id、名称、数目|

- **返回示例**
> 
{
  "msg": "success",
  "code": 200,
  "roleAndCount": [
    {
      "role_name": "开发组",
      "count": 11,
      "id": "1c28280eac5543a58b252d8e71cb6f51"
    }
  ]
}

#### 6. 统计考场各种状态考生数目

- **请求URL**
> [/examEmployee/statistics/all](#)

- **请求方式** 
>**GET**

- **请求参数**
>| 请求参数      |     参数类型 |   参数说明   | 参数需要
| :-------- | :--------| :------ |:------
| examId|  Long| 考试id| required|

- **返回参数**
> | 返回参数      |     参数类型 |   参数说明   |
| :-------- | :--------| :------ |
| msg|   boolean|  请求成功与否|
| code|   Integer|  执行结果code|
| countMap| Array[Model]| 考场内考试状态的考生|

- **返回示例**
> 
**```success```**
{
  "msg": "success",
  "code": 200,
  "countMap": {
    "all_count": 11,
    "is_send_message_count": 0,
    "is_send_email_count": 8,
    "confirm_count": 1,
    "give_up_count": 0
  }
}

#### 7. 考生修改考试状态

- **请求URL**
> [/examEmployee/confirm](#)

- **请求方式** 
>**GET**

- **请求参数**
>| 请求参数      |     参数类型 |   参数说明   | 参数需要
| :-------- | :--------| :------ |:------
| examId|  Long| 考试id| required|
| employeeId| String| 考生id| required|
| status| String| 考生确认状态 **-N未查看 T-已查看未确认 S-已确认 F-已放弃**| required|

- **返回参数**
> | 返回参数      |     参数类型 |   参数说明   |
| :-------- | :--------| :------ |
| msg|   boolean|  请求成功与否|
| code|   Integer|  执行结果code|
| countMap| Array[Model]| 考场内考试状态的考生|

- **返回示例**
> 
**```success```**
{
  "msg": "考生que'ren'zhuan'ta",
  "code": 200
}
**```failed```**
'''考试时间已过期'''
{
  "msg": "操作失败，考试不存在，可能已取消",
  "code": 500
}

#### 8. 查询考场内考生

- **请求URL**
> [/examEmployee/search](#)

- **请求方式** 
>**GET**

- **请求参数**
>| 请求参数      |     参数类型 |   参数说明   | 参数需要
| :-------- | :--------| :------ |:------
| examId|  Long| 考试id| required|
| username| String| 考生账号| optional|
| isSendEmail| String| 是否邮件通知| optional|
| checkflag| String| 考生确认状态 **-N未查看,T-已查看未确认,S-已确认,F-已放弃**| optional|
| status| String| 考生答题状态 **U-未答题,P-答题中,D-已交卷,R- 已生成报告**|optional|
| name| String| 考生姓名| optional|
| phone| String| 考生电话| optional|
| email| String| 考生邮箱| optional|
| pageNo| Long| 页码| required|
| pageSize| Long| 页大小| required|


- **返回参数**
> | 返回参数      |     参数类型 |   参数说明   |
| :-------- | :--------| :------ |
| msg|   boolean|  请求成功与否|
| code|   Integer|  执行结果code|
| countMap| Array[Model]| 考场内考试状态的考生|

- **返回示例**
> 
**```success```**
{
   "msg": "success",
   "code": 200,
   "examEmployees": [
     {
        "phone": "15989042436",
        "name": "谢水",
        "roleName": "开发组",
        "isSendEmail": "Y",
        "employeeId": "0e38ed24aef140dd97137c0df5184c2c",
        "email": "953843047@qq.com",
        "username": "hrd74245",
        "checkFlag": "F",
        "status": "D"
    }
  ]
}
**```failed```**
'''考试id参数不存在'''
{
  "msg": "考试参数不存在",
  "code": 400
}

### 题库管理
#### 1. 题库试题添加

- **请求URL**
> [/question/insert](#)

- **请求方式** 
>**POST**

- **请求参数**
>| 请求参数      |     参数类型 |   参数说明   | 参数需要
| :-------- | :--------| :------ |:------
| departmentId| String| 企业id| required|
| type| Integer| 试题类型| required|
| source| String| 试题来源| required|
| answer| String| 试题答案| required|
| content| String| 试题题干| required|
| pointId| String| 参考知识点| optional|
| labels| String| 试题标签id，多个以'&#124;'分割| optional|
| options| String| 试题选项，多个以'&#124;'分割| optional|
| remark| String| 试题备注| optional|

- **返回参数**
> | 返回参数      |     参数类型 |   参数说明   |
| :-------- | :--------| :------ |
| msg|   boolean|  请求成功与否|
| code|   Integer|  执行结果code|

- **返回示例**
> 
**```success```**
'''重复试题提交不会插入，但返回成功'''
{
  "msg": "success",
  "code": 200
}
**```failed```**
'''格式错误'''
{
  "msg": "题目格式错误",
  "code": 500
}

#### 2. 题库试题删除

- **请求URL**
> [/question/delete](#)

- **请求方式** 
>**POST**

- **请求参数**
>| 请求参数      |     参数类型 |   参数说明   | 参数需要
| :-------- | :--------| :------ |:------
| questionIds| Array[Long]| 问题id列表| required|


- **返回参数**
> | 返回参数      |     参数类型 |   参数说明   |
| :-------- | :--------| :------ |
| msg|   boolean|  请求成功与否|
| code|   Integer|  执行结果code|

- **返回示例**
> 
**```success```**
{
  "msg": "success",
  "code": 200
}

#### 3. 题库试题详情获取

- **请求URL**
> [/question/query/{questionId}](#)

- **请求方式** 
>**GET**

- **请求参数**
>| 请求参数      |     参数类型 |   参数说明   | 参数需要
| :-------- | :--------| :------ |:------
| questionId| Long| 问题id| required|


- **返回参数**
> | 返回参数      |     参数类型 |   参数说明   |
| :-------- | :--------| :------ |
| msg|   boolean|  请求成功与否|
| code|   Integer|  执行结果code|
| question| Model| 问题详情|

- **返回示例**
> 
**```success```**
{
  "msg": "success",
  "code": 200,
  "question": {
    "id": 67,
    "departmentId": "02eb40b714534f5c86ba246779af4bda",
    "type": "1",
    "source": "AI",
    "answer": "1|0|0|0",
    "content": "什么是______，这是我们课程中最为重要的一个概念，有必要加以专门界定。",
    "pointId": "99407.0.0.1-0.0",
    "createTime": "2018-08-29 15:42:10",
    "remark": null,
    "labels": null,
    "labelNames": null,
    "options": "素质测评|开发性测评|素质水平|参照性测评"
  }
}

#### 4. 题库试题更新

- **请求URL**
> [/question/update](#)

- **请求方式** 
>**POST**

- **请求参数**
>| 请求参数      |     参数类型 |   参数说明   | 参数需要
| :-------- | :--------| :------ |:------
| id| Long| 试题id| required|
| departmentId| String| 企业id| required|
| type| Integer| 试题类型| required|
| source| String| 试题来源| required|
| answer| String| 试题答案| required|
| content| String| 试题题干| required|
| pointId| String| 参考知识点| optional|
| labels| String| 试题标签id，多个以'&#124;'分割| optional|
| options| String| 试题选项，多个以'&#124;'分割| optional|
| remark| String| 试题备注| optional|


- **返回参数**
> | 返回参数      |     参数类型 |   参数说明   |
| :-------- | :--------| :------ |
| msg|   boolean|  请求成功与否|
| code|   Integer|  执行结果code|

- **返回示例**
> 
**```success```**
'''重复试题更新不会插入，但返回成功'''
{
  "msg": "success",
  "code": 200
}
**```failed```**
'''格式错误'''
{
  "msg": "题目格式错误",
  "code": 500
}
'''试题不存在'''
{
  "timestamp": "2018-08-29 19:22:14",
  "status": 500,
  "error": "Internal Server Error",
  "exception": "com.jobreading.common.exception.JrException",
  "message": "试题不存在",
  "path": "/question/update"
}
'''试题重复'''
{
  "msg": "更新失败：题库中存在相同题目，您可以在题库中搜索添加到试卷题库",
  "code": 500
}


#### 5. 试题知识点查找

- **请求URL**
> [/question/queryPoint/{questionId}](#)

- **请求方式** 
>**POST**

- **请求参数**
>| 请求参数      |     参数类型 |   参数说明   | 参数需要
| :-------- | :--------| :------ |:------
| questionId| Long| 问题id| required|


- **返回参数**
> | 返回参数      |     参数类型 |   参数说明   |
| :-------- | :--------| :------ |
| msg|   boolean|  请求成功与否|
| code|   Integer|  执行结果code|
| point| String| 知识点|

- **返回示例**
> 
**```success```**
{
  "msg": "success",
  "code": 200,
  "point": "99407.0.1.0-14.0"
}

#### 6. 题库试题搜索

- **请求URL**
> [/question/queryPoint/{questionId}](#)

- **请求方式** 
>**POST**

- **请求参数**
>| 请求参数      |     参数类型 |   参数说明   | 参数需要
| :-------- | :--------| :------ |:------
| departmentId| String| 问题id| required|
| questionIds| Array[Long]| 试题id列表| optional|
| questionId| Long| 试题id| optional|
| deleted| Integer| 试题可用状态| optional|
| label| String| 标签内容| optional|
| keyWord| String| 题干关键词| optional|
| beginTime| Date| 出题时间起始时间| optional|
| endTime| Date| 出题时间结束时间| optional|


- **返回参数**
> | 返回参数      |     参数类型 |   参数说明   |
| :-------- | :--------| :------ |
| msg|   boolean|  请求成功与否|
| code|   Integer|  执行结果code|
| questionList| Array[Model]| 试题详情列表|

- **返回示例**
> 
**```success```**
{
   "msg": "success",
   "code": 200,
   "questionList": [
      {
         "id": 2,
         "departmentId": "02eb40b714534f5c86ba246779af4bda",
         "type": "2",
         "source": "AF",
         "answer": "1|0|1|0",
         "content": "一个管理者所处层次越高，面临的情况越复杂，就越无先例可寻，就越需具备：",
         "pointId": null,
         "createTime": "2018-08-26 09:55:51",
         "remark": null,
         "labels": "43",
         "labelNames": "管理者",
         "options": "组织技能|组织技能|组织技能|组织技能"
      },
      {
         "id": 3,
         "departmentId": "02eb40b714534f5c86ba246779af4bda",
         "type": "3",
         "source": "AF",
         "answer": "T",
         "content": "群体决策的最大优点是集思广益和不浪费时间",
         "pointId": null,
         "createTime": "2018-08-28 17:42:06",
         "remark": null,
         "labels": "43",
         "labelNames": "管理者",
         "options": ""
      }
    ]
}
**```failed```**
{
  "msg": "参数错误",
  "code": 500
}

### 邮件服务
#### 1. 按选中考生发送

- **请求URL**
> [/mailService/sendByIds](#)

- **请求方式** 
>**POST**

- **请求参数**
>| 请求参数      |     参数类型 |   参数说明   | 参数需要
| :-------- | :--------| :------ |:------
| examId| Long| 考试id| required|
| employeeIds| Array[string]| 考生id| required|


- **返回参数**
> | 返回参数      |     参数类型 |   参数说明   |
| :-------- | :--------| :------ |
| msg|   boolean|  请求成功与否|
| code|   Integer|  执行结果code|

- **返回示例**
> 
**```success```**
{
  "msg": "success",
  "code": 200,
}
#### 2. 按考生确认状态批量发送邮件

- **请求URL**
> [/mailService/sendByStatus](#)

- **请求方式** 
>**POST**

- **请求参数**
>| 请求参数      |     参数类型 |   参数说明   | 参数需要
| :-------- | :--------| :------ |:------
| examId| Long| 考试id| required|
| status| Integer| 考生状态 **1-未确认 2-未发送 3-未完成 4-全部**| required|


- **返回参数**
> | 返回参数      |     参数类型 |   参数说明   |
| :-------- | :--------| :------ |
| msg|   boolean|  请求成功与否|
| code|   Integer|  执行结果code|

- **返回示例**
> 
**```success```**
{
  "msg": "success",
  "code": 200,
}

### 标签管理
### 考试报告
