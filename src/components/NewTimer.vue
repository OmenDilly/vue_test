<template>
    <div
        class="add__card"
    >
        <!-- кнопка для добавления нового таймера -->
        <span
            v-if="!newTimer"
            @click="newTimer = true"
            class="add__button material-icons"
        >
            <p>
                add
            </p>
        </span>
        <!-- форма добавления таймера -->
        <div 
            v-if="newTimer"
            class="new__timer"
        >
            <div 
                class="time__input"
            >
                <!-- поле часов -->
                <div 
                    class="time__unit hours"
                    id='hours'
                >
                    <span 
                        class="up material-icons"
                        id='increase'
                        @click="hours++"
                    >
                        expand_less
                    </span>
                    <input
                        max="24"
                        min="0" 
                        type="number"
                        id='type'
                        maxlength="2"
                        v-model="hours"
                    >
                    <span 
                        class="down material-icons"
                        id='decrease'
                        @click="hours--"
                    >
                        expand_more
                    </span>
                </div>
                <!-- поле минут -->
                <div class="time__unit minutes">
                    <span 
                        class="up material-icons"
                        id='increase'
                        @click="minutes++"
                    >
                        expand_less
                    </span>
                    <input
                        max="59"
                        min="0"
                        step="5" 
                        type="number" 
                        maxlength="2"
                        v-model="minutes"
                    >
                    <span 
                        class="down material-icons"
                        id='decrease'
                        @click="minutes--"
                    >
                        expand_more
                    </span>
                </div>
                <!-- поле секунд -->
                <div class="time__unit seconds">
                    <span 
                        class="up material-icons"
                        id='increase'
                        @click="seconds++"
                    >
                        expand_less
                    </span>
                    <input 
                        max="59"
                        step="5"
                        min="0"
                        type="number" 
                        id=type
                        v-model="seconds"
                    >
                    <span 
                        class="down material-icons"
                        id='decrease'
                        @click="seconds--"
                    >
                        expand_more
                    </span>
                </div>
            </div>

            <div class="add__actions">
                <!-- кнопка подтверждения добавления таймера -->
                <span 
                    @click.prevent="submit"
                    class="stop__button material-icons"
                >
                    done
                </span>
                <!-- кнопка отмены добавления -->
                <span 
                    @click="newTimer = false"
                    class="close__button material-icons"
                >
                    close
                </span>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                seconds: 0,
                minutes: 0,
                hours: 0,
                newTimer: false
            }
        },
        watch: {
            // проверка значений на корректность
            seconds(val) {
                if (!val) {
                    this.seconds = 0
                }
                if (val > 59) {
                    this.seconds = 0
                    this.minutes++
                }
                if (val < 0) {
                    this.seconds = 59
                    this.minutes--
                }
            },
            minutes(val) {
                if (!val) {
                    this.minutes = 0
                }
                if (val > 59) {
                    this.minutes = 0
                    this.hours++
                }
                if (val < 0) {
                    this.minutes = 59
                    this.hours--
                }
            },
            hours(val) {
                if (!val) {
                    this.hours = 0
                }
                if (val > 24) {
                    this.hours = 24
                }
                if (val < 0) {
                    this.hours = 0
                }
            }
        },
        methods: {
            // функция подтверждения создания нового таймера
            submit() {
                // формирование объекта
                const new_timer = {
                    id: Date.now(),
                    defaultValues: {
                        hours: parseInt(this.hours),
                        minutes: parseInt(this.minutes),
                        seconds: parseInt(this.seconds)
                    },
                    values: {
                        hours: parseInt(this.hours),
                        minutes: parseInt(this.minutes),
                        seconds: parseInt(this.seconds)
                    },
                    active: false,
                    interval: null,
                    expired: false
                }
                // отправка запроса на исполнение функции создания таймера
                this.$emit("add-timer", new_timer)
                this.newTimer = false
                // очистка полей ввода
                this.hours = 0
                this.minutes = 0
                this.seconds = 0
            }
        }
    }
</script>

<style scoped>
    /* главнй контейнер */
    .add__card {
        background-color: #696969;
        color: #9E9E9E;
        display: grid;
        align-items: center;
        justify-items: center;
        height: 120px;
        width: 225px;
    }

    /* кнопка добавления */
    .add__button {
        font-size: 30px;
        justify-self: stretch;
        align-self: stretch;
        display: grid;
        align-items: center;
        justify-items: center;
        cursor: pointer;
        transition: all .3s;
    }

    /* поля ввода */

    .time__input {
        display: grid;
        grid-template-columns: repeat(3, 1fr);
    }
    .time__input .time__unit {
        display: grid;
        justify-items: center;
        align-items: center;
        grid-template-columns: 1fr;
    }

    .time__unit span {
        /* font-size: 10px;  */
        user-select: none;
    }

    .time__input .time__unit.hours {
        justify-self: end;
    }
    
    .time__input .time__unit.minutes {
        justify-self: center;
    }

    .time__input .time__unit.seconds {
        justify-self: start;
    }

    .time__unit input {
        text-align: center;
        max-width: 25px;
        background: transparent;
        border: none;
        outline: none;
        color: #9E9E9E;
        max-height: 25px;
        font-size: 25px;
    }

    input[type=number]::-webkit-inner-spin-button,
    input[type=number]::-webkit-outer-spin-button
    {
        -webkit-appearance: none;
        margin: 0;
    }

    /* форма */
    .new__timer {
        display: grid;
        grid-row: repeat(2, 1fr);
        align-self: stretch;
        justify-self: stretch;
    }
    
    /* кнопки формы */
    .new__timer span {
        cursor: pointer;
        transition: all .3s;
        font-size: 30px;
    }

    .add__actions {
        display: grid;
        border-top: solid #9E9E9E 2px;
        grid-template-columns: repeat(2, 1fr);
        align-items: center;
        justify-items: center;
    }
    
    /* стили наведения на кнопки */
    .new__timer span:hover {
        color: white;
        align-items: center;
        justify-items: center;
        transform: scale(1.2);
    }

    .add__button:hover {
        background-color: #9E9E9E;
        color: white;
    }


</style>