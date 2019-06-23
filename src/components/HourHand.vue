<template>
  <div>
    <ClockHand :type="'hour'" :time="timeInMinutes"></ClockHand>
  </div>
</template>

<script>
import ClockHand from './ClockHand'

export default {
  name: 'HourHand',
  components: {
    ClockHand
  },
  props: ['time'],
  computed: {
    timeInMinutes() {
      const hours = this.time.hours > 12 ? (this.time.hours - 12) : this.time.hours
      return (hours*5) + this.minutesOffest
    },
    minutesOffest() {
      return (this.time.minutes / 60) * 5
    }
  },
  data() {
    return {
      valueCopy: 0
    }
  },
  watch: {
    valueCopy(newVal) {
      let hours = (newVal / 5)
      let mins = (hours % 1)*60
      this.time.minutes = mins
      this.time.hours = Math.floor(hours)
    }
  }
}
</script>