<template>

  <div class="hand" ref="hand" :class="[{'grabbing': isGrabbing}, type]" :style="transform" @mousedown="isGrabbing=true" @touchstart="isGrabbing=true">
  </div>

</template>

<script>

export default {

    name: 'ClockHand',
    props: ['type', 'time'],
    data() {
        return {
            isGrabbing: false,
            degrees: 180,
            center_x: 172,
            center_y: 172
        }
    },
    computed: {
        transform() {
            return { transform: 'rotate(' + this.degrees + 'deg)'}
        }
    },
    methods: {
        minutesToDegrees(minutes) {
            const positiveDegrees = minutes * 6
            return positiveDegrees - 180
        },
        degreesToMinutes(degrees) {
            const positiveDegrees = degrees + 180
            return positiveDegrees / 6
        },
        trackMouse(evt) {
            let parentBox = this.$parent.$parent.$refs.clock.getBoundingClientRect()
            let mouse_x = 0
            let mouse_y = 0
            if (evt.type == 'touchmove') {
                mouse_x = (evt.touches[0].pageX - parentBox.left)
                mouse_y = (evt.touches[0].pageY - parentBox.top)
            } else {
                mouse_x = (evt.pageX - parentBox.left)
                mouse_y = (evt.pageY - parentBox.top)
            }
            
            let radians = Math.atan2(mouse_x - this.center_x, mouse_y - this.center_y)

            let degrees = (radians * (180 / Math.PI) * -1)

            this.degrees = degrees
            this.$parent.valueCopy = this.degreesToMinutes(degrees)
        }
    },
    mounted() {
        if (!this.disabled) {
            window.addEventListener('mouseup', (e) => {
                this.isGrabbing = false
            })
            window.addEventListener('touchend', (e) => {
                this.isGrabbing = false
            })
            window.addEventListener('mousemove', (e) => {
                if (this.isGrabbing) {
                    this.trackMouse(e)
                }
            })
            window.addEventListener('touchmove', (e) => {
                if (this.isGrabbing) {
                    this.trackMouse(e)
                }
            })
        }
        this.degrees = this.minutesToDegrees(this.time)
    },
    watch: {
        time(newVal) {
            this.degrees = this.minutesToDegrees(newVal)
        }
    }
}
</script>
