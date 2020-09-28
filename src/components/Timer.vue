<template>
    <div 
        class="timer__card" 
        v-bind:class="{active: timer.active}"
    >
        <!-- вывод значений таймера -->
        <p
            class="value"
        >
            {{parsedTimer.parsed}}
        </p>
        <div 
            class="card__actions"
        >
            <!-- кнопка остановки таймера -->
            <span 
                v-if="timer.active"
                class="pause__button material-icons"
                @click="unActive"
            >
                pause
            </span>
            <!-- кнопка запуска таймера -->
            <span 
                v-else
                class="play__button material-icons"
                v-bind:class="{disabled: parsedTimer.expired}"
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
            },
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
                this.timer.expired = false
            }

        },
        computed: {
            // функция для корректного отображения значений таймера
            parsedTimer() {
                let expired = this.timer.expired
                let hours = this.timer.values.hours
                let minutes = this.timer.values.minutes
                let seconds = this.timer.values.seconds
                let pHours = hours >= 10 ? hours : "0" + hours
                let pMinutes = minutes >= 10 ? minutes : "0" + minutes
                let pSeconds = seconds >= 10 ? seconds : "0" + seconds
                let parsed = `${hours > 0 ? pHours + ":" : ""}${(minutes > 0 || hours > 0) ? pMinutes + ":" : ""}${pSeconds}`
                if (parseInt(parsed) === 0) {
                    expired = true
                }
                return {parsed, expired}

            }
        },
    }
</script>

<style scoped>

    /* главный контейнер */
    .timer__card {
        background-color: #696969;
        color: #9E9E9E;
        font-size: 25px;
        display: grid;
        transition: all .3s;
        grid-template-rows: repeat(2, 60px);
    }

    .timer__card:hover {
        transform: translateY(-2px);
        /* box-shadow: 0px 15px 54px -16px rgba(0,0,0,0.3); */
        box-shadow: 0px 14px 29px -9px rgba(0, 0, 0, 0.233);
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
        transition: all .3s cubic-bezier(0, 0.77, 0.76, 2.26);
        user-select: none;
    }

    .disabled {
        cursor: default;
        pointer-events: none;
    }

    /* наведение на конпку */
    .card__actions span:hover {
        /* transform: scale(1.2); */
    }

    .delete__button {
        /* transition: transform .3s cubic-bezier(0, 0.77, 0.76, 2.26) */
    }

    .delete__button:hover {
        transform: rotate(-90deg) scale(1.2);
        color: #E1A9B9;
        /* color: white; */
    }

    .play__button:hover {
        transform: scale(1.2);
        color: #BAE1C4;
    }
    .pause__button:hover {
        transform: scale(1.2);
        color: #B0C3E1;
    }
    .pause__button:active {
        transform: rotate(-45deg);
    }
    .play__button:active {
        transform: rotate(45deg);
    }

    .stop__button:hover {
        transform: scale(1.2);
        color: white;
    }

    /* стили запущенного таймера */
    .active {
        color: white;
    }

    .active .stop__button:hover {
        color: #9E9E9E;
    }
    .active .delete__button:hover {
        color: #9E9E9E;
    }

    .active .card__actions {
        border-color: white;
    }

    /* .active span:hover {
        transform: scale(1);
        border-color: #9E9E9E;
        color: #9E9E9E;
    } */
    
</style>