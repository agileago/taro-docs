---
title: Taro.addInterceptor(interceptor)
sidebar_label: addInterceptor
---

> 最低 Taro 版本: 1.2.16

可以使用拦截器在请求发出前或发出后做一些额外操作。

在调用 `Taro.request` 发起请求之前，调用 `Taro.addInterceptor` 方法为请求添加拦截器，拦截器的调用顺序遵循洋葱模型。
拦截器是一个函数，接受 chain 对象作为参数。chain 对象中含有 **requestParmas** 属性，代表请求参数。拦截器内最后需要调用 `chain.proceed(requestParams)` 以调用下一个拦截器或发起请求。

Taro 提供了两个内置拦截器 `logInterceptor` 与 `timeoutInterceptor`，分别用于打印请求的相关信息和在请求超时时抛出错误。

支持情况：<img title="微信小程序" src={require('@site/static/img/platform/weapp.png').default} className="icon_platform" width="25px"/> <img title="百度小程序" src={require('@site/static/img/platform/swan.png').default} className="icon_platform" width="25px"/> <img title="支付宝小程序" src={require('@site/static/img/platform/alipay.png').default} className="icon_platform" width="25px"/> <img title="字节跳动小程序" src={require('@site/static/img/platform/tt.png').default} className="icon_platform" width="25px"/> <img title="QQ 小程序" src={require('@site/static/img/platform/qq.png').default} className="icon_platform" width="25px"/> <img title="H5" src={require('@site/static/img/platform/h5.png').default} className="icon_platform" width="25px"/> <img title="React Native" src={require('@site/static/img/platform/rn.png').default} className="icon_platform icon_platform--not-support" width="25px"/>

## 类型

```tsx
(interceptor: interceptor) => any
```

## 参数

| 参数 | 类型 |
| --- | --- |
| interceptor | `interceptor` |

## 示例代码

### 示例 1

```tsx
const interceptor = function (chain) {
  const requestParams = chain.requestParams
  const { method, data, url } = requestParams

  console.log(`http ${method || 'GET'} --> ${url} data: `, data)

  return chain.proceed(requestParams)
    .then(res => {
      console.log(`http <-- ${url} result:`, res)
      return res
    })
  }
Taro.addInterceptor(interceptor)
Taro.request({ url })
```

### 示例 2

```tsx
Taro.addInterceptor(Taro.interceptors.logInterceptor)
Taro.addInterceptor(Taro.interceptors.timeoutInterceptor)
Taro.request({ url })
```
