<template>
  <div>
    <slot
      :days="days"
      :hours="hours"
      :minutes = "minutes"
      :seconds = "seconds"
      :milliseconds = "milliseconds"
      :totalDays = "totalDays"
      :totalHours = "totalHours"
      :totalMinutes = "totalMinutes"
      :totalSeconds = "totalSeconds"
      :totalMilliseconds = "totalMilliseconds"
      :countDownMilliSeconds="countDownMilliSeconds"
    >
    </slot>
  </div>
</template>

<script>
const MILLISECONDS_SECOND = 1000
const MILLISECONDS_MINUTE = 60 * MILLISECONDS_SECOND
const MILLISECONDS_HOUR = 60 * MILLISECONDS_MINUTE
const MILLISECONDS_DAY = 24 * MILLISECONDS_HOUR

export default {
  name: 'CountDown',
  props: {
    // 倒计时毫秒数
    countDownMilliSeconds: {
      type: Number,
      default: 0
    },
    // 是否自动开启倒计时
    autoStart: {
      type: Boolean,
      default: true
    },
    // 倒计时间隔时间
    interval: {
      type: Number,
      default: 1000,
      validator: value => value >= 0
    },
    // 是否将事件的消息发送出去
    isEmit: {
      type: Boolean,
      default: false
    }
  },
  data () {
    return {
      isCounting: false,
      // 记录剩余的总共的毫秒数
      currentMilliseconds: 123123123
    }
  },
  computed: {
    // 倒计时还剩的天数
    days () {
      return Math.floor(this.currentMilliseconds / MILLISECONDS_DAY)
    },
    // 1 天内倒计时还剩的小时数，小于 24
    hours () {
      return Math.floor((this.currentMilliseconds % MILLISECONDS_DAY) / MILLISECONDS_HOUR)
    },
    // 1 小时内倒计时还剩的分钟数，小于 60
    minutes () {
      return Math.floor((this.currentMilliseconds % MILLISECONDS_HOUR) / MILLISECONDS_MINUTE)
    },
    // 1 分钟内倒计时还剩的秒数，小于 60
    seconds () {
      return Math.floor((this.currentMilliseconds % MILLISECONDS_MINUTE) / MILLISECONDS_SECOND)
    },
    // 1 秒内倒计时还剩的毫秒数，小于 1000
    milliseconds () {
      return Math.floor(this.currentMilliseconds % MILLISECONDS_SECOND)
    },
    // 倒计时总共还剩的天数
    totalDays () {
      return this.days
    },
    // 倒计时总共还剩的小时数
    totalHours () {
      return Math.floor(this.currentMilliseconds / MILLISECONDS_HOUR)
    },
    // 倒计时总共还剩的分钟数
    totalMinutes () {
      return Math.floor(this.currentMilliseconds / MILLISECONDS_MINUTE)
    },
    // 倒计时总共还剩的秒数
    totalSeconds () {
      return Math.floor(this.currentMilliseconds / MILLISECONDS_SECOND)
    },
    // 倒计时总共还剩的毫秒数
    totalMilliseconds () {
      return this.currentMilliseconds
    }
  },
  methods: {
    start () {
      // 如果已经在倒计时，直接返回
      if (this.isCounting) {
        return
      }

      this.isCounting = true

      // 如果需要 emit 事件
      if (this.isEmit) {
        this.$emit('start')
      }

      this.continue()
    },
    continue () {
      if (!this.isCounting) {
        return
      }

      const gap = Math.min(this.currentMilliseconds, this.interval)

      if (gap > 0) {
        this.timeout = setTimeout(this.progress, gap, this)
      } else {
        this.end()
      }
    },
    progress () {
      if (!this.isCounting) {
        return
      }

      this.currentMilliseconds -= this.interval

      // 如果需要 emit 事件，同时倒计时还没有结束，emit progress 事件
      if (this.isEmit && this.currentMilliseconds > 0) {
        this.$emit('progress', {
          days: this.days,
          hours: this.hours,
          minutes: this.minutes,
          seconds: this.seconds,
          totalDays: this.totalDays,
          totalHours: this.totalHours,
          totalMinutes: this.totalMinutes,
          totalSeconds: this.totalSeconds,
          totalMilliseconds: this.totalMilliseconds
        })
      }

      this.continue()
    },
    pause () {
      clearTimeout(this.timeout)
    },
    end () {
      if (!this.isCounting) {
        return
      }

      this.pause()
      this.currentMilliseconds = 0
      this.isCounting = false

      if (this.isEmit) {
        this.$emit('end')
      }
    }
  },
  watch: {
    $prop: {
      deep: true,
      immediate: true,
      handler () {
        this.currentMilliseconds = this.countDownMilliSeconds

        if (this.autoStart) {
          this.$nextTick(() => {
            this.start()
          })
        }
      }
    }
  },
  beforeDestroy () {
    this.pause()
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
