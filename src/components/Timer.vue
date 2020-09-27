<template>
    <div 
        class="timer__card" 
        v-bind:class="{active: timer.active}"
    >
        <!-- вывод значений таймера -->
        <p
            class="value"
        >
            {{parsedTimer}}
        </p>
        <div 
            class="card__actions"
        >
            <!-- кнопка остановки таймера -->
            <span 
                v-if="timer.active"
                class="play__button material-icons"
                @click="unActive"
            >
                pause
            </span>
            <!-- кнопка запуска таймера -->
            <span 
                v-else
                class="play__button material-icons"
                @click="setActive"
            >
                play_arrow
            </span>
            <!-- кнопка сброса таймера -->
            <span 
                class="stop__button material-icons"
                @click="resetTimer"
            >
                stop
            </span>
            <!-- кнопка удаления таймера -->
            <span 
                class="delete__button material-icons"
                @click="$emit('delete-timer', timer.id)"
            >
                close
            </span>
        </div>
    </div>
</template>

<script>
    export default {
        // получение данных о таймере от родительского компонента
        props: {
            timer: {
                type: Object,
                required: true
            }
        },
        methods: {
            // отправка запросов родительскому компоненту на исполнение функций
            setActive() {
                this.$emit("set-active", this.timer.id)
                this.timer.active = true
            },
            unActive() {
                this.$emit("set-unactive", this.timer.id)
                this.timer.active = false
            },
            resetTimer() {
                this.$emit("reset", this.timer.id)
            }

        },
        computed: {
            // функция для корректного отображения значений таймера
            parsedTimer() {
                let hours = this.timer.values.hours
                let minutes = this.timer.values.minutes
                let seconds = this.timer.values.seconds
                let pHours = hours >= 10 ? hours : "0" + hours
                let pMinutes = minutes >= 10 ? minutes : "0" + minutes
                let pSeconds = seconds >= 10 ? seconds : "0" + seconds
                let parsed = `${hours > 0 ? pHours + ":" : ""}${(minutes > 0 || hours > 0) ? pMinutes + ":" : ""}${pSeconds}`
                // let parsed = `${pHours}:${pMinutes}:${pSeconds}`
                return parsed

            }
        }
    }
</script>

<style scoped>

    /* главный контейнер */
    .timer__card {
        background-color: #696969;
        color: #9E9E9E;
        font-size: 25px;
        display: grid;
        grid-template-rows: repeat(2, 60px);
    }

    /* значение таймера */
    .value {
        font-weight: 400;
        align-self: center;
        text-align: center;
    }

    /* контейнер кнопок */
    .card__actions {
        display: grid;
        grid-template-columns: repeat(3, 1fr);
        align-items: center;
        border-top: solid #9E9E9E 2px;
    }

    /* кнопки */
    .card__actions span {
        cursor: pointer;
        font-size: 30px;
        justify-self: center;
        transition: all .3s;
    }

    /* наведение на конпку */
    .card__actions span:hover {
        transform: scale(1.2);
        color: white;
    }

    /* стили запущенного таймера */
    .active {
        color: white;
    }

    .active .card__actions {
        border-color: white;
    }

    .active span:hover {
        transform: scale(1);
        border-color: #9E9E9E;
        color: #9E9E9E;
    }
    
</style>