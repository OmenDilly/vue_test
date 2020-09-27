<template>
  <div id="app" >
    <!-- вывод списка таймеров -->
    <TimerList 
      v-bind:timers="timers"
      @delete-timer="deleteTimer"
      @add-timer="addTimer"
      @set-active="setActive"
      @reset="resetTimer"
      @set-unactive="unActive"
    />
  </div>
</template>

<script>
  import TimerList from "@/components/TimerList"

  export default {
    name: "App",
    // данные для работы
    data() {
      return {
        // массив таймеров
        timers: [],
      }
    },
    components: {
      TimerList
    },
    methods: {
      // удаление таймера
      deleteTimer(id) {
        let activeTimer = this.timers.find(timer => timer.id == id).interval
        clearInterval(activeTimer)
        this.timers = this.timers.filter(timer => timer.id !== id)
      },
      // добавление таймера
      addTimer(timer) {
        this.timers.push(timer)
      },
      // остановка таймера
      unActive(id) {
        let activeTimer = this.timers.find(timer => timer.id == id).interval
        clearInterval(activeTimer)
      },
      // сброс таймера
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
      },
      // запуск таймера
      setActive(id) {
        // поиск таймера по идентификатору
        let activeTimer = this.timers.find(item => item.id === id)

        // функция запуска найденного таймера
        const startTimer = () => {
          // начало отсчета
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
              activeTimer.values.seconds = 59
              activeTimer.values.hours--
            }
          }
          // остановка таймера при окончании отсчета
          if (activeTimer.values.hours == 0 && activeTimer.values.minutes == 0 && activeTimer.values.seconds == 0) {
            clearInterval(this.onTimer);
            activeTimer.active = false
          }

        }
        // запуск функции отсчета
        activeTimer.interval = setInterval(startTimer, 1000)
      }

    }
  }
</script>

<style>

  /* стили по-умолчанию */
  body {
    font-family: "Roboto", sans-serif;
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
