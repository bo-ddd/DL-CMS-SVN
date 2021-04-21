<h3>
	<center>dl-cms第一期接口文档</center>    
</h3>

#### baseUrl:

 http://192.168.1.18/7001
 
### 测试账号：
 账号：woodfish1   密码：999999

#### 登录接口定义

1. 接口名： /user/signin;

2. 描述：  此接口用来进行cms登录；

3. 入参：  
   ```javascript
   var data = { 
     username:[String],
     password:[String],
     captcha:'',  //[String]图形验证码,非必填项
     version:'V1.0'  //[String]非必填项，如果传 V1.0,需要加图形验证码参数
   }
   ```

4. 出参：
    ```javascript
    var res = {
      status:[Number]      //登录是否成功 1：成功      0：失败；
      message:[String]      //返回信息
      data:[String jwtToken] 
    }
    ```
5. 登录失效和未登录
  ```javascript
  //登录失效
  var res = {
	data:{
	  status: '9001',
	  message: 'token验证失败',
	  data: false
	}
  };
  //未登录
  var res = {
	data:{
	  status: '9001',
	  message: 'token验证失败',
	  data: false
	}
  };
  ```


#### 获取用户信息接口

1. 接口名称： /user/info

2. 接口描述：用来获取用户相关信息；

3. 接口入参：

   ```javascript
   var request = {}
   ```

4. 接口出参:

   ```javascript
   var res = {
       "status": 1,   //[Number] 判断是否查询成功 1：成功 0：失败
       "message": "success",   // [String]判断是否查询成功  success:成功  fail:失败
       "data": {
           "userId": 4,   //[Number]用户id primaryKey;
           "userName": "woodfish1",   //[String]用户名称
           "phoneNumber": "123345",   //[String]手机号码
           "price": 0,				 //[Number] 账户余额
           "uuid": "9624150f-00a5-49d7-abdb-e8855910cb1c"  //唯一标识
       }
   }
   ```

5. 获取订单列表
  1. 接口名称：/order/list
  2. 描述：获取订单列表
  3. 接口入参：
  ```javascript
  var request = {
    pageNum:1, //[Number]当前第几页
    pageSize: 20,  //[Number] 每页展示多少条数据,非必填项，如不传，会默认展示20条
    orderId:"",  //非必填
    phoneNumber:''  // 非必填 手机号
  }
  ```
  4. 接口出参：
  ```javascript
  var res = {
    "count": 2,  //数据总条数
    "countPage":5  //总页数
    "rows": [
        {
            "orderId": 1,   //
            "phoneNumber": "13333333333",
            "orderType": 1,  //1:话费  2：流量
            "packageType": 1,  // 1代表1元套餐，x代表 x元套餐
            "price": 1,   //实付价格
            "orderStatus": 1,  // 1:已完成  0:待审核
            "createdAt": "2021-04-07T11:24:16.000Z", //订单生成时间
            "updatedAt": null  //订单修改时间
        },
        {
            "orderId": 2,
            "phoneNumber": "13444444444",
            "orderType": 1,
            "packageType": 1,
            "price": 1,
            "orderStatus": 1,
            "createdAt": "2021-04-07T11:54:36.000Z",
            "updatedAt": null
        }
    ]
}
  ```
6. 注册账号
  1. 接口名称： /user/create
  2. 描述：注册账号接口
  3. 接口入参：
  ```javascript
  var request = {
    username:'woodfish', //[String]用户名，最少6位
    password: 999999;,  //[String] 用户名密码 最少6位
    phoneNumber:''  //[String]手机号
  }
  ```
  4. 接口出参：
  ```javascript 
  var res = {
    code:1,  //1成功  0：失败
    message:'success',  //提示信息
    data:result
  }
  ```
### 创建订单接口
  1. 接口名称： /order/create
  2. 描述：创建订单接口
  3. 接口入参：
  ```javascript
  var request = {
    packageType:1, //[String]1：1元套餐，  2：2元套餐  3：3元套餐；
    phoneNumbers:[]  //[Array]手机号的集合
  }
  ```
  4. 接口出参：
  ```javascript 
  var res = {
    status:1,  // 1成功   4:余额不足
    message:'订单生成中....' 
    }
  ``` 

### 获取用户列表接口
  1. 接口名称：/user/list
  2. 描述：获取用户列表,此接口需要有管理员权限
  3. 接口入参：
  ```javascript
  var request = {
    pageNum:1, //[Number]当前第几页
    pageSize: 20,  //[Number] 每页展示多少条数据,非必填项，如不传，会默认展示20条
    userId:"",  //非必填
    phoneNumber:''  // 非必填 手机号
  }
  ```
  4. 接口出参：
  ```javascript
  var res = {
    "count": 2,  //数据总条数
    "countPage":5  //总页数
    "rows": [
        {
            "userId": 1,   //
            "phoneNumber": "13333333333",
            "price": 1,   //账户余额
	    "identity":1   //  1:管理员  0：普通商户
            "createdAt": null, //用户创建时间
            "updatedAt": null  //修改用户信息时间
        },
        {
            "userId": 2,   //
            "phoneNumber": "13333333333",
            "price": 1,   //账户余额
	    "identity":1   //  1:管理员  0：普通商户
            "createdAt": null, //用户创建时间
            "updatedAt": null  //修改用户信息时间
        }
    ]
}
  ```
  ### 修改用户信息接口
  1. 接口名称： /user/update
  2. 描述： 适用于用户中心修改用户信息接口
  3. 接口入参：
  ```javascript
  var request = {
    phoneNumber:'', //[String]手机号
    password:''
  }
  ```
  4. 接口出参：
  ```javascript 
  var res = {
    status:1,  //1成功  0失败
    message:'信息修改成功',
    data:null
  }
  ``` 
  
### 充值余额接口
  1. 接口名称： /user/bill
  2. 描述： 适用于管理员给用户充值按钮；
  3. 接口入参：
  ```javascript
  var request = {
    userId:'',
    price:'', //[String]用户总价格；
  }
  ```
  4. 接口出参：
  ```javascript 
  var res = {
    status:1,  //1:成功  0：失败
    message:'充值成功！',
    data:null
  }
  ``` 
  
### 图形验证码
  1. 接口名称： /user/captcha
  2. 描述：适用于登录,注册时的获取图形验证码功能；
  3. 接口方式： 'GET'
  4. 接口入参： 无
  5. 接口出参：图片
 
 ### 校验图形验证码
  1. 接口名称： /user/checkCaptcha
  2. 描述： 适用于用户登录注册时的验证码， 失效时间60秒
  3. 接口入参：
  ```javascript
  var request = {
    captcha:'' //[String]4位字符
  }
  ```
  4. 接口出参：
  ```javascript 
  var res = {
    status:1,  //1:成功  0：失败
    message:'success',  //success  0:验证失败
    data:null
  }
  ``` 
 
 ### 增加充值日志
  1. 接口名称： /log/bill
  2. 描述： 用户充值后增加充值记录；
  3. 接口入参：
  ```javascript
  var request = {
    userName,//充值的用户名
    uuid,  //充值的uuid;
    price：''   //[Number]充值后的余额；
  }
  ```
  4. 接口出参：
  ```javascript 
  var res = {}  该接口是直接调用，不需要做任何处理；
  ``` 
  
  ### 充值日志列表
  1. 接口名称： /log/list
  2. 描述： 用户充值后增加充值记录；
  3. 接口入参：
  ```javascript
  var request = {
    pageNum:1, //[Number]当前第几页
    pageSize: 20,  //[Number] 每页展示多少条数据,非必填项，如不传，会默认展示20条
    userName:"",  //非必填
    uuid:''  // 非必填 用户uuid;
  }
  ```
  4. 接口出参：
  ```javascript
  var res = {
    "count": 2,  //数据总条数
    "countPage":5  //总页数
    "rows": [
        {
            "id": 1,   //
            "uuid": "13333333333",
            "price": 1,   //实付价格
            "createdAt": "2021-04-07T11:24:16.000Z", //订单生成时间
            "updatedAt": null  //订单修改时间
        }
    ]
}
  ```
  
  ### 审核订单
  1. 接口名称： /order/examine
  2. 描述： 审核订单接口；
  3. 接口入参：
  ```javascript
  var request = {
    orderId:''   //【string】 订单id
  }
  ```
  4. 接口出参：
  ```javascript
  var res = {}
  ```

