<template>
  <div id="app" >
    <TimerList v-bind:timers="timers"/>
  </div>
</template>

<script>
import TimerList from '@/components/TimerList'
export default {
  name: 'App',
  data() {
    return {
      timers: [
        {id: 1, value: '1000', active: true},
        {id: 2, value: '2000', active: true}
      ]
    }
  },
  components: {
    TimerList
  }
}
</script>

<style>
  * {
    transition: all 0.3s;
  }

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
