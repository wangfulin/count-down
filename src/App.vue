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

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
