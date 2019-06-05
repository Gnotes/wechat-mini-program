# 微信小程序备忘录

- [项目代码组成](#项目代码组成)
- [全局配置](#全局配置(app.json))
- [页面配置](#页面配置(*.json))
- [微信搜索索引](#微信搜索索引(sitemap.json))
- [项目代码组成](#项目代码组成)
- [App实例](#App实例)
- [Page实例](#Page实例)
- [自定义组件](#自定义组件)
- [路由导航](#路由导航)
- [API约定](#API约定)

## 项目代码组成

> 一个页面由以下4个配置页面组成：

- `.json` : 配置文件(*覆盖当前页面窗口样式*)
- `.wxml` : 模板文件
- `.wxss` : 样式文件
- `.js` : 业务逻辑文件

## 全局配置(app.json)

> 小程序 **根目录** 下的 `app.json` 文件用来对微信小程序进行 **全局配置** , [详细说明](https://developers.weixin.qq.com/miniprogram/dev/reference/configuration/app.html)

## 页面配置(*.json)

> 页面配置项在当前页面会覆盖 `app.json` 的 **window** 中相同的配置项,  
> **只** 能设置 `window` 对应的配置项，以决定本页面的窗口表现，所以无需写 window 这个属性 , [详细说明](https://developers.weixin.qq.com/miniprogram/dev/reference/configuration/page.html)

## 微信搜索索引(sitemap.json)

> 配置微信小程序搜索索引的配置规则，[详细说明](https://developers.weixin.qq.com/miniprogram/dev/reference/configuration/sitemap.html)

## App实例

> App() 必须在 app.js 中调用，必须调用且只能调用一次，[详细说明](https://developers.weixin.qq.com/miniprogram/dev/reference/api/App.html)

### 生命周期及内建函数

| 属性 | 类型 | 默认值 | 必填 | 说明 |
| --- | --- | --- | --- | --- |
| onLaunch | function | - | 否 | 生命周期回调——监听小程序初始化 |
| onShow | function | - | 否 | 生命周期回调——监听小程序启动或切前台 |
| onHide | function | - | 否 | 生命周期回调——监听小程序切后台 |
| onError | function | - | 否 | 错误监听函数 |
| onPageNotFound | function | - | 否 | 页面不存在监听函数 |

### 获取全局实例对象

> 整个小程序 **只有一个 App 实例**，是全部页面共享的。可以通过 `getApp` 方法获取到全局唯一的 App 实例，[详细说明](https://developers.weixin.qq.com/miniprogram/dev/reference/api/getApp.html)

## Page实例

> 注册小程序中的一个页面，其指定页面的初始数据、生命周期回调、事件处理函数等，[详细说明](https://developers.weixin.qq.com/miniprogram/dev/reference/api/Page.html)

| 属性 | 类型 | 默认值 | 必填 | 说明 |
| --- | --- | --- | --- | --- |
| data | Object | - | - | 页面的初始数据 |
| onLoad | function | - | - | 生命周期回调—监听页面加载 |
| onShow | function | - | - | 生命周期回调—监听页面显示 |
| onReady | function | - | - | 生命周期回调—监听页面初次渲染完成 |
| onHide | function | - | - | 生命周期回调—监听页面隐藏 |
| onUnload | function | - | - | 生命周期回调—监听页面卸载 |
| onPullDownRefresh | function | - | - | 监听用户下拉动作 |
| onReachBottom | function | - | - | 页面上拉触底事件的处理函数 |
| onShareAppMessage | function | - | - | 用户点击右上角转发 |
| onPageScroll | function | - | - | 页面滚动触发事件的处理函数 |
| onResize | function | - | - | 页面尺寸改变时触发，详见 响应显示区域变化 |
| onTabItemTap | function | - | - | 当前是 tab 页时，点击 tab 时触发 |
| 其他 | any | - | - | 开发者可以添加任意的函数或数据到 Object 参数中，在页面的函数中用 this 可以访问 |

### 获取当前页面栈

> 通过 getCurrentPages 返回获取，数组中第一个元素为首页，*最后一个* 元素为 **当前页面**

注⚠️：
- 不要尝试修改页面栈，会导致路由以及页面状态错误。
- 不要在 App.onLaunch 的时候调用 getCurrentPages()，此时 page 还没有生成。

## 自定义组件

### Component

[详细说明](https://developers.weixin.qq.com/miniprogram/dev/reference/api/Component.html)

### Behavior

[详细说明](https://developers.weixin.qq.com/miniprogram/dev/reference/api/Behavior.html)

## 路由导航

| 路由方式 | API方式 | 组件方式 |
| --- | --- | --- |
| 打开新页面 | `wx.navigateTo` | `<navigator open-type="navigateTo"/>` |
| 页面重定向 | `wx.redirectTo` |`<navigator open-type="redirectTo"/>` |
| 页面返回 | `wx.navigateBack` |`<navigator open-type="navigateBack"/>` |
| Tab 切换 | `wx.switchTab` | `<navigator open-type="switchTab"/>` |
| 重启 | `wx.reLaunch` | `<navigator open-type="reLaunch"/>` |

[详细说明](https://developers.weixin.qq.com/miniprogram/dev/framework/app-service/route.html)

## API约定

① `on` 开头的 API 用来监听某个事件是否触发  
② 以 `Sync` 结尾的 API 都是同步 API  
③ 大多异步 API 接口通常都接受一个 Object 类型的参数，包含：`success`、`fail`、`complete`