# **目录**

 [initSDK](#a0)

 [showLogin](#a1)

 [isLogin](#a_isLogin)

 [logout](#a2)

 [showItemById](#a3)

 [showItemByUrl](#a4)

 [openOrderList](#a6)

 [openNavigationPage](#a7)

 [openSearchResult](#a8)

 [openShoppingCart](#a10)



# 准备

1. 进入京东开普勒（https://k.jd.com/）
2. 注册登录，并在控制台创建一个应用
3. 选择创建的应用，在页面左侧选择【能力申请】，申请导购能力
4. 在页面左侧选择【SDK下载】，根据自己的实际bundleid与安卓的apk包来生成专有的SDK，并下载SDK
5. 下载并解压京东开普勒 安全图片模块。[点击下载]()
6. 解压  **步骤4**  所下载的iOS SDK，复制 **Kepler.bundle** 到 **步骤5** 中的以下路径替换同名文件``/mKeplerPic_iOS/mKeplerPic/target``
7. 解压  **步骤4**  所下载的Android SDK，复制``/src/main/res/raw``下的 **safe.jpg** 到 **步骤5** 中的以下路径替换同名文件``//mKeplerPic_Android/mKeplerPic/res_mKeplerPic/res/raw``
8. 分别压缩 **步骤6** 与 **步骤7**各自的mKeplerPic目录为zip包
9. 打开apicloud控制台，并选择你的应用
10. 依次点击：左侧菜单【模块】—>右侧顶部【自定义模块】
11. 模块名称填入mKeplerPic，并分别上传 **步骤8** 生成的zip包，注意对应
12. 保存模块，并添加mKeplerPic模块

#  配置

## 需要在config.xml配置如下信息，并上传编译来生效

```xml
<preference name="querySchemes" value="tmall,tbopen,jdlogin,openapp.jdmobile" />
<feature name="mKepler">
    <param name="urlScheme" value="sdkback + appKey" />
    <param name="appKey" value="appKey" />
    <param name="appSecret" value="appSecret" />
</feature>
```

<div id="a0"></div>

# **initSDK**

初始化开普勒SDK
initSDK(callback(ret, err))

## callback(ret, err)

ret：

- 类型：JSON对象
- 内部字段：

```js
{
    code: '0',
    message: 'success'
}
```

err：

- 类型：JSON对象
- 内部字段：

```js
{
    code: '1000',                   //错误码
    message: 'user is not exist'      //错误描述
}
```

## 示例代码

```js
var mKepler = api.require('mKepler');
mKepler.initSDK(function(ret, err) {
    if (ret) {
        alert('success：' + JSON.stringify(ret));
    } else {
        alert('error：' + JSON.stringify(err));
    }
});
```

## 可用性

iOS系统，Android系统
可提供的1.0.0及更高版本

<div id="a1"></div>

# **showLogin**

打开京东授权登陆
showLogin(callback(ret, err))

## callback(ret, err)

ret：

- 类型：JSON对象
- 内部字段：

```js
{
    code: '1',
    message: 'success'
}
```

err：

- 类型：JSON对象
- 内部字段：

```js
{
    code : '1000',                   //错误码
    message:'user is not exist'      //错误描述
}
```

## 示例代码

```js
var mKepler = api.require('mKepler');
mKepler.showLogin(function(ret, err) {
    if (ret) {
        alert('success：' + JSON.stringify(ret));
    } else {
        alert('error：' + JSON.stringify(err));
    }
});
```

## 可用性

iOS系统，Android系统
可提供的1.0.0及更高版本

<div id="a_isLogin"></div>

# **isLogin**

判断是否授权登录
isLogin(callback(ret, err))

## callback(ret, err)

ret：

- 类型：JSON对象
- 内部字段：

```js
{
    code: '1',  // 1为已经授权
    message: 'success'
}
```

err：

- 类型：JSON对象
- 内部字段：

```js
{
    code : '0',                   //错误码
    message:'not login'      //错误描述
}
```

## 示例代码

```js
var mKepler = api.require('mKepler');
mKepler.isLogin(function(ret, err) {
    if (ret) {
        alert('success：' + JSON.stringify(ret));
    } else {
        alert('error：' + JSON.stringify(err));
    }
});
```

## 可用性

iOS系统，Android系统
可提供的1.0.0及更高版本

<div id="a2"></div>

# **logout**

取消授权
logout(callback(ret, err))

## callback(ret, err)

ret：

- 类型：JSON对象
- 内部字段：

```js
{
    code: '0' ,
    message: '取消授权成功'
}
```

err：

- 类型：JSON对象
- 内部字段：

```js
{
    code : '90000',            //错误码
    message: '未授权'           //错误描述
}
```

## 示例代码

```js
var mKepler = api.require('mKepler');
mKepler.logout(function(ret, err) {
    if (ret) {
        alert('success：' + JSON.stringify(ret));
    } else {
        alert('error：' + JSON.stringify(err));
    }
});
```

## 可用性

iOS系统，Android系统
可提供的1.0.0及更高版本

<div id="a3"></div>

# **showItemById**

通过SKU打开单品页
showItemById({params},callback(ret, err))

## params

itemID:

- 类型：字符串
- 描述：商品的SKU，如 https://item.jd.com/3791763.html 中为3791763

isOpenByH5:

- 类型：布尔型
- 描述：（可选项）是否已html5的方式打开，false为打开京东APP

processColor:

- 类型：字符串
- 描述：（可选项）进度条颜色，iOS有效

backTagID:

- 类型：字符串
- 描述：（可选项）打开京东后显示的返回按钮

openType:

- 类型：字符串
- 描述：（可选项）打开的H5进入的动画类型，取值范围 push、present

customParams:

- 类型：JSON 对象
- 描述：（可选项）传参数据为第三方应用自定义,可以为页面,频道标识;也可以标识分成信息;该数据只做统计需求。（不建议传入中文以及特殊字符） **\* 禁止传参带入以下符号：   =#%&+?<{}**

actId:

- 类型：字符串
- 描述：（可选项）设置ActId 京东达人内容ID

ext:

- 类型：字符串
- 描述：（可选项）内容渠道扩展字段

virtualAppkey:

- 类型：字符串
- 描述：（可选项）计费到另外一个账号体系的appkey（为空或不传则计入到当前SDK申请的账号下）

position:

- 类型：字符串
- 描述：（可选项）计费参数，目前安卓有效

## 示例代码

```js
var mKepler = api.require('mKepler');
var param = {
    itemID : '4675712',
    isOpenByH5: false,
    processColor: '#000',
    backTagID: '',
    openType: 'push',
    customParams: {}
};
mKepler.showItemById(param);
```

## 可用性

iOS系统，Android系统
可提供的1.0.0及更高版本

<div id="a4"></div>

# **showItemByUrl**

通过URL打开任意商品页面
showItemByUrl({params},callback(ret, err))

## params

url:

- 类型：字符串
- 描述：商品的页面url，如 https://item.jd.com/3791763.html

isOpenByH5:

- 类型：布尔型
- 描述：（可选项）是否已html5的方式打开，false为打开京东APP

processColor:

- 类型：字符串
- 描述：（可选项）进度条颜色，iOS有效

backTagID:

- 类型：字符串
- 描述：（可选项）打开京东后显示的返回按钮

openType:

- 类型：字符串
- 描述：（可选项）打开的H5进入的动画类型，取值范围 push、present

customParams:

- 类型：JSON 对象
- 描述：（可选项）传参数据为第三方应用自定义,可以为页面,频道标识;也可以标识分成信息;该数据只做统计需求。（不建议传入中文以及特殊字符） **\* 禁止传参带入以下符号：   =#%&+?<{}**

actId:

- 类型：字符串
- 描述：（可选项）设置ActId 京东达人内容ID

ext:

- 类型：字符串
- 描述：（可选项）内容渠道扩展字段

virtualAppkey:

- 类型：字符串
- 描述：（可选项）计费到另外一个账号体系的appkey（为空或不传则计入到当前SDK申请的账号下）

position:

- 类型：字符串
- 描述：（可选项）计费参数，目前安卓有效

## 示例代码

```js
var mKepler = api.require('mKepler');
var param = {
    url : 'https://item.jd.com/3791763.html',
    isOpenByH5: false,
    processColor: '#000',
    backTagID: '',
    openType: 'push',
    customParams: {}
};
mKepler.showItemByUrl(param);
```

## 可用性

iOS系统，Android系统
可提供的1.0.0及更高版本


<div id="a6"></div>

# **openOrderList**

 打开订单列表
openOrderList(callback(ret, err))

## params

isOpenByH5:

- 类型：布尔型
- 描述：（可选项）是否已html5的方式打开，false为打开京东APP

processColor:

- 类型：字符串
- 描述：（可选项）进度条颜色，iOS有效

backTagID:

- 类型：字符串
- 描述：（可选项）打开京东后显示的返回按钮

openType:

- 类型：字符串
- 描述：（可选项）打开的H5进入的动画类型，取值范围 push、present

customParams:

- 类型：JSON 对象
- 描述：（可选项）传参数据为第三方应用自定义,可以为页面,频道标识;也可以标识分成信息;该数据只做统计需求。（不建议传入中文以及特殊字符） **\* 禁止传参带入以下符号：   =#%&+?<{}**

actId:

- 类型：字符串
- 描述：（可选项）设置ActId 京东达人内容ID

ext:

- 类型：字符串
- 描述：（可选项）内容渠道扩展字段

virtualAppkey:

- 类型：字符串
- 描述：（可选项）计费到另外一个账号体系的appkey（为空或不传则计入到当前SDK申请的账号下）

position:

- 类型：字符串
- 描述：（可选项）计费参数，目前安卓有效

## 示例代码

```js
var mKepler = api.require('mKepler');
var param = {
    isOpenByH5: false,
    processColor: '#000',
    backTagID: '',
    openType: 'push',
    customParams: {}
};
mKepler.openOrderList(param);
```

## 可用性

iOS系统，Android系统
可提供的1.0.0及更高版本

<div id="a7"></div>

# **openNavigationPage**

打开导航页
openNavigationPage(callback(ret, err))

## params

isOpenByH5:

- 类型：布尔型
- 描述：（可选项）是否已html5的方式打开，false为打开京东APP

processColor:

- 类型：字符串
- 描述：（可选项）进度条颜色，iOS有效

backTagID:

- 类型：字符串
- 描述：（可选项）打开京东后显示的返回按钮

openType:

- 类型：字符串
- 描述：（可选项）打开的H5进入的动画类型，取值范围 push、present

customParams:

- 类型：JSON 对象
- 描述：（可选项）传参数据为第三方应用自定义,可以为页面,频道标识;也可以标识分成信息;该数据只做统计需求。（不建议传入中文以及特殊字符） **\* 禁止传参带入以下符号：   =#%&+?<{}**

actId:

- 类型：字符串
- 描述：（可选项）设置ActId 京东达人内容ID

ext:

- 类型：字符串
- 描述：（可选项）内容渠道扩展字段

virtualAppkey:

- 类型：字符串
- 描述：（可选项）计费到另外一个账号体系的appkey（为空或不传则计入到当前SDK申请的账号下）

position:

- 类型：字符串
- 描述：（可选项）计费参数，目前安卓有效

## 示例代码

```js
var mKepler = api.require('mKepler');
var param = {
    isOpenByH5: false,
    processColor: '#000',
    backTagID: '',
    openType: 'push',
    customParams: {}
};
mKepler.openNavigationPage(param);
```

## 可用性

iOS系统，Android系统
可提供的1.0.0及更高版本

<div id="a8"></div>

# **openSearchResult**

根据搜索关键字打开搜索结果页
openSearchResult({params},callback(ret, err))

## params

searchKey:

- 类型：字符串
- 描述：搜索关键字

isOpenByH5:

- 类型：布尔型
- 描述：（可选项）是否已html5的方式打开，false为打开京东APP

processColor:

- 类型：字符串
- 描述：（可选项）进度条颜色，iOS有效

backTagID:

- 类型：字符串
- 描述：（可选项）打开京东后显示的返回按钮

openType:

- 类型：字符串
- 描述：（可选项）打开的H5进入的动画类型，取值范围 push、present

customParams:

- 类型：JSON 对象
- 描述：（可选项）传参数据为第三方应用自定义,可以为页面,频道标识;也可以标识分成信息;该数据只做统计需求。（不建议传入中文以及特殊字符） **\* 禁止传参带入以下符号：   =#%&+?<{}**

actId:

- 类型：字符串
- 描述：（可选项）设置ActId 京东达人内容ID

ext:

- 类型：字符串
- 描述：（可选项）内容渠道扩展字段

virtualAppkey:

- 类型：字符串
- 描述：（可选项）计费到另外一个账号体系的appkey（为空或不传则计入到当前SDK申请的账号下）

position:

- 类型：字符串
- 描述：（可选项）计费参数，目前安卓有效

## 示例代码

```js
var mKepler = api.require('mKepler');
var param = {
    searchKey: 'iphone',
    isOpenByH5: false,
    processColor: '#000',
    backTagID: '',
    openType: 'push',
    customParams: {}
};
mKepler.openSearchResult(param);
```

## 可用性

iOS系统，Android系统
可提供的1.0.0及更高版本


<div id="a10"></div>

# **openShoppingCart**

打开购物车界面
openShoppingCart(callback(ret, err))

## params

isOpenByH5:

- 类型：布尔型
- 描述：（可选项）是否已html5的方式打开，false为打开京东APP

processColor:

- 类型：字符串
- 描述：（可选项）进度条颜色，iOS有效

backTagID:

- 类型：字符串
- 描述：（可选项）打开京东后显示的返回按钮

openType:

- 类型：字符串
- 描述：（可选项）打开的H5进入的动画类型，取值范围 push、present

customParams:

- 类型：JSON 对象
- 描述：（可选项）传参数据为第三方应用自定义,可以为页面,频道标识;也可以标识分成信息;该数据只做统计需求。（不建议传入中文以及特殊字符） **\* 禁止传参带入以下符号：   =#%&+?<{}**

actId:

- 类型：字符串
- 描述：（可选项）设置ActId 京东达人内容ID

ext:

- 类型：字符串
- 描述：（可选项）内容渠道扩展字段

virtualAppkey:

- 类型：字符串
- 描述：（可选项）计费到另外一个账号体系的appkey（为空或不传则计入到当前SDK申请的账号下）

position:

- 类型：字符串
- 描述：（可选项）计费参数，目前安卓有效

## 示例代码

```js
var mKepler = api.require('mKepler');
var param = {
    isOpenByH5: false,
    processColor: '#000',
    backTagID: '',
    openType: 'push',
    customParams: {}
};
mKepler.openShoppingCart(param);
```

## 可用性

iOS系统，Android系统
可提供的1.0.0及更高版本