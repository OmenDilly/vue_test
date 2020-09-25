<template>
  <div id="app" >
    <Timer v-bind:key='timer.id' v-for='timer of timers' v-bind:timer='timer'/>
            <div class="add__container">
            <span class="add__button">
                <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="black" width="18px" height="18px"><path d="M0 0h24v24H0z" fill="none"/><path d="M19 13h-6v6h-2v-6H5v-2h6V5h2v6h6v2z"/></svg>
            </span>
        </div>
  </div>
</template>

<script>
import Timer from '@/components/Timer'
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
    Timer
  }
}
</script>

<style>
  body {
    box-sizing: border-box;
    outline: none;
    margin: 0;
    padding: 0;
    background-color: #353638;
    display: grid;
  }
  #app {
    display: grid;
    gap: 10px;
    align-self: center;
    justify-self: center;
    /* height: 100%; */
    /* justify-items: center; */
    /* align-content: space-around; */
    /* align-items: center; */
    /* justify-content:space-evenly; */
    align-items: stretch;
    justify-items: stretch;
    grid-template-columns: 200px 200px;
  }
</style>
