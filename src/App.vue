<template>
  <div id="app" >
    <TimerList 
      v-bind:timers="timers"
      @delete-timer='deleteTimer'
      @add-timer='addTimer'
      @set-active='setActive'
      @reset='resetTimer'
      @set-unactive='unActive'
    />
  </div>
</template>

<script>
import TimerList from '@/components/TimerList'
export default {
  name: 'App',
  data() {
    return {
      timers: [],
    }
  },
  components: {
    TimerList
  },
  methods: {
    deleteTimer(id) {
      let activeTimer = this.timers.find(timer => timer.id == id).interval
      clearInterval(activeTimer)
      this.timers = this.timers.filter(timer => timer.id !== id)
    },
    addTimer(timer) {
      this.timers.push(timer)
    },
    unActive(id) {
      let activeTimer = this.timers.find(timer => timer.id == id).interval
      clearInterval(activeTimer)
    },
    resetTimer(id) {
      let targetTimer = this.timers.find(item => item.id == id)
      const defaultHours = targetTimer.defaultValues.hours
      const defaultMinutes = targetTimer.defaultValues.minutes
      const defaultSeconds = targetTimer.defaultValues.seconds
      targetTimer.values = {
        hours: defaultHours,
        minutes: defaultMinutes,
        seconds: defaultSeconds
      }
      targetTimer.active = false
      clearInterval(targetTimer.interval)
      console.log(this.onTimer, id)
    },
    setActive(data) {
      console.log(data.active)
      let activeTimer = this.timers.find(item => item.id === data.id)


        const startTimer = () => {

          console.log(activeTimer.values.seconds)

          if (activeTimer.values.seconds != 0) {
            activeTimer.values.seconds--
          }

          if (activeTimer.values.seconds == 0) {
            if (activeTimer.values.minutes != 0) {
              activeTimer.values.seconds = 59
              activeTimer.values.minutes--
            }
          }
          if (activeTimer.values.minutes == 0) {
          if (activeTimer.values.hours != 0) {
              activeTimer.values.minutes = 59
              activeTimer.values.hours--
            }
          }
            if (activeTimer.values.hours == 0 && activeTimer.values.minutes == 0 && activeTimer.values.seconds == 0) {
              clearInterval(this.onTimer);
              activeTimer.active = false
            }

        }
        activeTimer.interval = setInterval(startTimer, 1000)
      
    }

  }
}
</script>

<style>
  body {
    font-family: 'Roboto', sans-serif;
    box-sizing: border-box;
    outline: none;
    margin: 0;
    padding: 0;
    background-color: #353638;
  }
  #app {
    display: grid;
  }
</style>
