<template>
  <div id="app" >
    <TimerList 
      v-bind:timers="timers"
      @delete-timer='deleteTimer'
      @add-timer='addTimer'
      @set-active='setActive'
      @reset='resetTimer'
    />
  </div>
</template>

<script>
import TimerList from '@/components/TimerList'
export default {
  name: 'App',
  data() {
    return {
      timers: [

      ]
    }
  },
  components: {
    TimerList
  },
  methods: {
    deleteTimer(id) {
      this.timers = this.timers.filter(timer => timer.id !== id)
    },
    addTimer(timer) {
      this.timers.push(timer)
    },
    resetTimer(id) {
      let targetTimer = this.timers.find(item => item.id === id)
      const defVal = targetTimer.defaultValues
      targetTimer.values = defVal
      
    },
    setActive(data) {
      console.log(data.active)
      let onTimer
      let activeTimer = this.timers.find(item => item.id === data.id)


        const startTimer = () => {

          console.log(activeTimer.values.seconds)

          if (activeTimer.values.seconds != 0) {
            // activeTimer.values.seconds = 59
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
          // if (data.active) {
            if (activeTimer.values.hours == 0 && activeTimer.values.minutes == 0 && activeTimer.values.seconds == 0) {
              clearInterval(onTimer);
              activeTimer.active = false
              // alert("Reached zero");
            }
          // }

        }
        onTimer = setInterval(startTimer, 1000);
      
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
