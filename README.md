# vue-grid-password

> A grid password vue component

# Demo
[![手机扫描二维码查看](http://oq8q06ybp.bkt.clouddn.com/image/qrCode.png)](http://60kmlh.ink/vue-GridPassword/)


```sh
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build

````
## Usage
```javascript
# somewhere
import GridPassword from '../components/GridPassword'

# in your component
components: {
    GridPassword
  }
```
```html
<template>
  <div>
    <GridPassword 
     :passwordLength='gridNum' 
     :onConfirm='onConfirm' 
     :onClose='onClose' 
     :isNumber='isNumber'
     :isPassword='isPassword'
     :isBtn='isBtn'>
    </GridPassword>
  </div>
<template/>
```

#### Props
Name | type | default | description
---:| --- | ---| ---
tip | String | '请输入密码' | 输入提示语
passwordLength | Number | 6 | 格子位数
isPassword | Boolean | true | 显示明文或者密码黑点
isNumber | Boolean | true | 调出数字键盘或者混合键盘
isBtnCtr | Boolean | true | 使用确认按钮或者自动提交

#### Events
Name | isRequire | description
---:| --- | --- 
onConfirm | require | 输入完成时的回调函数
onClose | require | 关闭输入框的回调函数

## License
Copyright (c) 2017 60kmlh
Licensed under the MIT license.