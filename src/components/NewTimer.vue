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
                    <span class="up"></span>
                    <input
                        max='24'
                        min='0' 
                        type="number" 
                        v-model='time.hours'
                    >
                    <span class="down"></span>
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
                    active: false
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
        max-width: 30px;
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
/* 
    input[type=number]::-webkit-inner-spin-button,
    input[type=number]::-webkit-outer-spin-button
    {
        -webkit-appearance: none;
        margin: 0;
    } */

    .new__timer {
        display: grid;
        /* grid-template-columns: repeat(2, 1fr); */
        grid-row: repeat(2, 1fr);
        align-self: stretch;
        justify-self: stretch;
        /* align-items: center;
        justify-items: center; */
    }

    .new__timer span {
        cursor: pointer;
        transition: all .3s;
    }

    .add__actions {
        display: grid;
        grid-template-columns: repeat(2, 1fr);
        align-items: center;
        justify-items: center;
    }
    

    .time__input {
        display: grid;
        align-items: center;
        justify-items: center;
        grid-template-columns: repeat(3, 1fr);
    }

    .new__timer span:hover {
        color: white;
        align-items: center;
        justify-items: center;
        transform: scale(1.2);
    }

    .new__timer input {
    }

    .add__button:hover {
        background-color: #9E9E9E;
        color: white;
    }


</style>