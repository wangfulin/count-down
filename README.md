# vue-component-popup

> 弹层组件

## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build

# build for production and view the bundle analyzer report
npm run build --report
```

## 功能介绍
该组件是一个倒计时组件：
1. countDownMilliSeconds: 倒计的的毫秒数
2. autoStart：是否开启倒计时
3. interval: 间隔多少更新倒计时
4. isEmit：是否发送相关的事件

## 示例
```
<template>
  <div id="app">
    <img src="./assets/logo.png" />
    <CountDown :countDownMilliSeconds="12312312312">
      <template slot-scope="props">
        <p>总共还有：{{props.days}} 天 {{props.hours}} 小时 {{props.minutes}} 分 {{props.seconds}} 秒 {{props.milliseconds}} 毫秒</p>
        <p>总共还剩：{{props.totalDays}} 天 </p>
        <p>总共还剩：{{props.totalHours}}小时</p>
        <p>总共还剩：{{props.totalMinutes}}分</p>
        <p>总共还剩：{{props.totalSeconds}}秒</p>
        <p>总共还剩：{{props.totalMilliseconds}}毫秒</p>
      </template>
    </CountDown>
  </div>
</template>

<script>
import CountDown from './components/CountDown'

export default {
  name: 'App',
  components: {
    CountDown
  }
}
</script>
```
## 展示
![](https://gw.alipayobjects.com/zos/rmsportal/rQNPaqGqLeLJmHyYaOVk.gif)

For a detailed explanation on how things work, check out the [guide](http://vuejs-templates.github.io/webpack/) and [docs for vue-loader](http://vuejs.github.io/vue-loader).
