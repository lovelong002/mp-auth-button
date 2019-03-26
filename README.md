 小程序授权登录按钮
插件说明 :
此插件仅支持在mpvue框架上使用，逻辑已经嵌入，亲们只需引入并在components里注册后即可使用，通过回调事件获取用户信息，按钮的文案及样式可以用户进行微调覆盖，使用相当方便简单，因为此按钮在整个项目中基本只有在一个地方出现，所以没有全局注册功能；使用方法如下:

1、下载
```
npm i mp-auth-button
```
2、在要使用的页面中引入并注册
```
import authButton from "mp-auth-button"			//组件名字自由定义
```
```
components: {
    authButton,
  },
```
3、注册后,在HTML中使用
```
 <authButton
  @showLoading="showLoadingFn"
  @success="authSuccess"
  :text="'授权登录'"
  :type="true"
  >
  </authButton>
```
4、获取授权成功后微信返回的用户信息（在methods中）
```
  authSuccess(val, callback) {
  		console.log(val)
		//val里有三个值 {
						//code: val.code,
						//iv: val.iv,
						//encrypted_data: val.encryptedData,
						 //}
		// 如果type为true的话,一定要在跟后端处理完逻辑后页面跳转时调用 callback(true),因为在插件内部给按钮做了点击节流,
		// 防止有些大佬狂点
		callback(true)
    },
```
5、添加加载中的动画,如果添加了,记得要在授权成功后调用 wx.hideLoading() 关闭（在methods中）
```
showLoadingFn() {
      wx.showLoading({
        title: '授权中...',
      });
    },
```
6、配置说明

1、showLoading 点击按钮后的加载中动画，可以自定义，可以不调用;

2、type 是否开启点击节流,防止有些用户狂点，不传的话默认为true，建议使用,因为在插件内部已经在最佳时机切入此形关;

3、succwss 成功获取用户信息后的回调，其中有两个参数，第一个是用户信息，第二个是callback(true)，名字随便写，但一定要传个true进去;

4、text 按钮文本,不传默认为 "授权登录"；

5、按钮样式可以使用自己找到类名去修改覆盖；






