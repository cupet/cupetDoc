# 接口文档
- 接口说明：
  - 1、请求header统一为：
  ```html
    Content-Type：application/x-www-form-urlencoded
   ```
  - 2、接口返回统一格式说明，stat、msg、data为所有接口比返回字段，后续仅只对data内容说明：
    ```html
      {
          "stat": 0,
          "msg": "交互成功",
          "data": null
      }
     ```
  - 3、出参stat状态说明：
    ```html
        	OK(0, "交互成功"),
        	PARAM_IS_NULL(-4, "必传参数为null"),
        	EXCEPTION(-2, "服务器异常"),
        
        	//login 异常
        	LOGIN_OPENID_NOT(-2001, "openid不存在"),
        	LOGIN_GET_TOKEN_EXCEPTION(-2002, "登录获取token异常"),
        
        	ARTICLE_ID_NOT_EXIST(-2101, "文章id不存在"),
        
        	//token 异常
        	TOKEN_REPET_LOGIN(-1001, "重复登录"),
        	CHECK_LOGIN_NOT_TOKEN_KEY(-1002, "验证token key不存在"),
        	CHECK_LOGIN_NOT_TOKEN(-1003, "验证token不存在"),
        	EXIT_LOGIN_NOT_TOKEN_KEY(-1002, "退出token key不存在"),
        	EXIT_LOGIN_NOT_TOKEN(-1003, "退出token不存在"),
        
        	//其他 异常
        	WX_CODE_JM_EXCEPTION(-6001, "微信code解密异常"),
        	WX_DATA_JM_EXCEPTION(-6002, "微信解密用户基础信息异常"),
        
        	FAULT(1, "交互失败");
    ```
  
# API 接口列表
- 后台管理接口（http://106.15.233.137:8035/qcj-background）

接口名称| HTTP方法|说明
-------|--------|------
/article/inserOrUpdateArticle|POST|插入或者更新文章接口
/article/deleteArticle|POST|删除文章接口
/article/queryAllArticle|POST|查询所有文章列表接口
/banner/inserOrUpdateBanner|POST|插入或者更新文章接口
/banner/deleteBanner|POST|删除文章接口
/banner/queryAllBanner|POST|查询所有文章列表接口

- 小程序接口（http://106.15.233.137:8025/wxsa-service）

接口名称| HTTP方法|说明
-------|--------|------
/wxUser/login|POST|小程序登、注册接口

# API 后台管理接口详细说明

- 1、插入或者更新文章接口
  - 接口url：/article/inserOrUpdateArticle
  - 接口入参：
  
  字段名| 类型|是否必传|含义
  -------|--------|------|-----
  id|Integer|是|主键id，插入时id传-1，更新时传文章id
  orderId|Integer|否|排序号，文章按照该字段排序，orderId一致时，按照更新时间排序
  title|String|是|文章标题
  coverUrl|String|否|封面图
  content|String|否|内容
  author|String|否|作者
  oneLevel|Integer|是|一级分类：1 猫咪、2：狗狗、 -1 未知
  twoLevel|String|否|二级分类
  status|Integer|是|状态：-1 未知、1 待发布、2 已发布
  
  - 接口出参，请参考统一的出参格式

- 2、删除文章接口
  - 接口url：/article/deleteArticle
  - 接口入参：
  
  字段名| 类型|是否必传|含义
  -------|--------|------|-----
  id|Integer|是|主键id
  
  - 接口出参，请参考统一的出参格式
  
- 3、查询文章列表接口
  - 接口url：/article/queryAllArticle
  - 接口入参：无
  - 接口出参：请参考接口返回统一格式说明，data内容字段说明如下：
  
    字段名| 类型|含义
    -------|--------|-----
    list|LevelDto列表|LevelDto的列表
    LevelDto|对象|
    levelId|Integer|一级分类id|
    levelName|String|分类名称
    list|ArticleDto列表|文章列表
    ArticleDto|对象|
    id|Integer|主键id，插入时id传-1，更新时传文章id
    orderId|Integer|排序号，文章按照该字段排序，orderId一致时，按照更新时间排序
    title|String|文章标题
    coverUrl|String|封面图
    content|String|内容
    author|String|作者
    oneLevel|Integer|一级分类：1 猫咪、2：狗狗、 -1 未知
    twoLevel|String|二级分类
    status|Integer|状态：-1 未知、1 待发布、2 已发布
    inserttime|Long|插入时间，毫秒的时间戳
    updatetime|Long|更新时间，毫秒的时间戳
  
- 4、插入或者更新轮播图接口
  - 接口url：/banner/inserOrUpdateBanner
  - 接口入参：
  
  字段名| 类型|是否必传|含义
  -------|--------|------|-----
  id|Integer|是|主键id，插入时id传-1，更新时传轮播图id
  orderId|Integer|否|排序号，按照该字段排序，orderId一致时，按照更新时间排序
  picUrl|String|是|图片url地址
  linkUrl|String|否|链接
  status|Integer|是|状态：-1 未知、1 待发布、2 已发布
  
  - 接口出参，请参考统一的出参格式

- 5、删除轮播图接口
  - 接口url：/banner/deleteBanner
  - 接口入参：
  
  字段名| 类型|是否必传|含义
  -------|--------|------|-----
  id|Integer|是|主键id
  
  - 接口出参，请参考统一的出参格式
  
- 6、查询轮播图列表接口
  - 接口url：/banner/queryAllBanner
  - 接口入参：无
  - 接口出参：请参考接口返回统一格式说明，data内容字段说明如下：
  
    字段名| 类型|含义
    -------|--------|-----
    list|List类型|狗狗的信息
    id|Integer|是|主键id
    orderId|Integer|否|排序号，按照该字段排序，orderId一致时，按照更新时间排序
    picUrl|String|是|图片url地址
    linkUrl|String|否|链接
    status|Integer|是|状态：-1 未知、1 待发布、2 已发布
    status|Integer|状态：-1 未知、1 待发布、2 已发布
    inserttime|Long|插入时间，毫秒的时间戳
    updatetime|Long|更新时间，毫秒的时间戳  
  
  
# 小程序接口
- 小程序登录、注册接口
  - 接口url：/wxUser/login
  - 接口入参：
  
    字段名| 类型|是否必传|含义
    -------|--------|------|-----
    code|String|是|小程序登录code
    encryptedData|String|否|用户基础信息的加密信息
    iv|String|否|用户基础信息的加密信息
    phoneEncryptedData|String|否|手机号的加密信息
    phoneIv|String|否|手机号的加密信息
    imei|String|否|设备号
  
  - 接口出参：请参考接口返回统一格式说明，data内容字段说明如下：
  
    字段名| 类型|含义
    -------|--------|-----
    accid|Integer|用户id
    token|String|用户登录token信息
  
  
  