<template>
    <div 
        class='timer__card' 
        v-bind:class='{active: timer.active}'
    >
        <p
            class='value'
        >
            {{timer.values.hours >= 10 ? timer.values.hours + ':' : 0 + timer.values.hours + ':'}}{{timer.values.minutes >= 10 ? timer.values.minutes + ':' : 0 + timer.values.minutes + ':'}}{{timer.values.seconds >= 10 ? timer.values.seconds : 0 + timer.values.seconds}}
        </p>

        <div 
            class='card__actions'
        >
            <span 
                class='play__button material-icons'
                @click='setActive'
            >
            {{!timer.active ? 'play_arrow' : 'pause'}}
                <!-- <input 
                    type="checkbox" 
                    id='media__button'
                    @change='timer.active = !timer.active'
                >
                <label for="media__button">{{!timer.active ? 'play_arrow' : 'pause'}}</label> -->
            </span>
            <span 
                class='stop__button material-icons'
                @click='resetTimer'
            >
                stop
            </span>
            <span 
                class='delete__button material-icons'
                @click="$emit('delete-timer', timer.id)"
            >
                close
            </span>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        timer: {
            type: Object,
            required: true
        }
    },
    methods: {
        setActive() {
            // console.log(this.timer.active)
            this.$emit('set-active', {id: this.timer.id, active: this.timer.active})
            this.timer.active = !this.timer.active
        },
        resetTimer() {
            this.$emit('reset', this.timer.id)
        }

    },
    mounted() {
        console.log(this.timer)
    }
}
</script>

<style scoped>
    .timer__card {
        background-color: #696969;
        color: #9E9E9E;
        font-size: 25px;
        display: grid;
        grid-template-rows: repeat(2, 60px);
    }

    .value {
        font-weight: 400;
        align-self: center;
        text-align: center;
    }

    .card__actions {
        display: grid;
        grid-template-columns: repeat(3, 1fr);
        align-items: center;
        border-top: solid #9E9E9E 2px;
    }

    .card__actions span {
        cursor: pointer;
        font-size: 30px;
        justify-self: center;
        transition: all .3s;
    }

    .card__actions span:hover {
        transform: scale(1.2);
        color: white;
    }
    
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