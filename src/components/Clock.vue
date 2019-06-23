<template>
    <div>
        <div ref="clock" class="clock" :style="{ 'background-image': 'url(' + require('@/assets/clock.png') + ')' }">
            <MinuteHand :time="time"></MinuteHand>
            <HourHand :time="time"></HourHand>
            <div class="center"></div>
        </div>
    </div>
</template>

<script>
import HourHand from './HourHand'
import MinuteHand from './MinuteHand'

export default {
    name: 'Clock',
    components: {
        HourHand,
        MinuteHand
    },
    props: ['time']
}
</script>

<style lang="scss">
  @import "@/assets/_clock.scss";
</style>

