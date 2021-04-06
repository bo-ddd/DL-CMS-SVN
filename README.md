<h3>
	<center>dl-cms第一期接口文档</center>    
</h3>

#### baseUrl:

 http://192.168.1.18/7001
 
### 测试账号：
 账号：woodfish1   密码：999999

#### 登录接口定义

1. 接口名： /user/signin ;

2. 描述：  此接口用来进行cms登录；

3. 入参：  
   ```javascript
   var data = { 
     username:[String],
     password:[String]
   }
   ```

4. 出参：
  ```javascript
    var res = {
      status:[Number]      //登录是否成功 1：成功      0：失败；
      message:[String]      //返回信息
    }
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

   

