<template>
  <div id="app">
    <clock :time="time"/>
  </div>
</template>

<script>
import Clock from './components/Clock'

export default {
  name: 'app',
  components: {
    Clock
  },
  data() {
    return {
      time: {
        hours: 10,
        minutes: 10
      }
    }
  }
}
</script>
