<template>
  <div>
    <ClockHand :type="'min'" :time="time.minutes"></ClockHand>
  </div>
</template>

<script>
import ClockHand from './ClockHand'

export default {
  name: 'MinuteHand',
  components: {
    ClockHand
  },
  props: ['time'],
  data() {
    return {
      valueCopy: 0
    }
  },
  watch: {
    valueCopy(newVal, oldVal) {
      this.time.minutes = newVal

      if (oldVal < 1 && newVal > 59) {
        if (this.time.hours == 0 || this.time.hours == null) this.time.hours = 11
        else this.time.hours--
      }
      if (oldVal > 59 && newVal < 1) {
        if (this.time.hours == 11) this.time.hours = 0
        else this.time.hours++
      }
    }
  }
}
</script>
