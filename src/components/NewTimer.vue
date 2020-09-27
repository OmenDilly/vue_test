<template>
    <div
        class="add__card"
    >
        <span
            v-if='!newTimer'
            @click='newTimer = true'
            class='add__button material-icons'
        >
            <p>
            add

            </p>
        </span>
        <div 
            v-if='newTimer'
            class='new__timer'
        >
            <div class="time__input">
                <div class="time__unit hours">
                    <span 
                        class="up material-icons"
                        @click='time.hours++'
                    >
                        expand_less
                    </span>
                    <input
                        max='24'
                        min='0' 
                        type="number" 
                        v-model='time.hours'
                    >
                    <span 
                        class="down material-icons"
                        @click='time.hours--'
                    >
                        expand_more
                    </span>
                </div>
                <div class="time__unit minutes">
                    <span class="up"></span>
                    <input
                        max='60'
                        min='0'
                        step='5' 
                        type="number" 
                        v-model='time.minutes'
                    >
                    <span class="down"></span>
                </div>
                <div class="time__unit seconds">
                    <span class="up"></span>
                    <input 
                        max='60'
                        step='5'
                        min='0'
                        type="number" 
                        v-model='time.seconds'
                    >
                    <span class="down"></span>
                </div>
            </div>

            <div class="add__actions">
                <span 
                    @click.prevent='submit'
                    class='stop__button material-icons'
                >
                    done
                </span>
                <span 
                    @click='newTimer = false'
                    class='close__button material-icons'
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
                time: {
                    seconds: '0',
                    minutes: '0',
                    hours: '0'
                },
                newTimer: false
            }
        },
        methods: {
            submit() {
                console.log(this.time)
                const new_timer = {
                    id: Date.now(),
                    defaultValues: {
                        hours: this.time.hours,
                        minutes: this.time.minutes,
                        seconds: this.time.seconds
                    },
                    values: {
                        hours: this.time.hours,
                        minutes: this.time.minutes,
                        seconds: this.time.seconds
                    },
                    active: false,
                    interval: null
                }
                this.$emit('add-timer', new_timer)
                this.newTimer = false
            }
        }
    }
</script>

<style scoped>
    .add__card {
        background-color: #696969;
        color: #9E9E9E;
        display: grid;
        align-items: center;
        justify-items: center;
        height: 120px;
        width: 225px;
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

    input[type=number]::-webkit-inner-spin-button,
    input[type=number]::-webkit-outer-spin-button
    {
        -webkit-appearance: none;
        margin: 0;
    }

    .new__timer {
        display: grid;
        grid-row: repeat(2, 1fr);
        align-self: stretch;
        justify-self: stretch;
    }

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
    
    

    .time__input {
        display: grid;
        /* align-items: center;
        justify-items: stretch; */
        grid-template-columns: repeat(3, 1fr);
    }
    .time__input .time__unit {
        display: grid;
        /* align-items: center; */
        justify-items: center;
        align-items: center;
        grid-template-columns: 1fr;

    }

    .time__unit span {
        font-size: 20px;
        /* align-self: center;
        border-top: 1px solid white; */
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