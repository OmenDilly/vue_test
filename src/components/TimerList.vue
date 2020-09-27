<template>
    <div class='card__container'>
        <Timer 
            v-for='timer of timers'
            v-bind:key='timer.id'
            v-bind:timer='timer'
            @delete-timer='deleteTimer'
            @set-active='setActive'
            @reset='resetTimer'
            @set-unactive='unActive'
        />
        <NewTimer
            @add-timer='addTimer'
        />

    </div>

</template>

<script>
import Timer from '@/components/Timer'
import NewTimer from '@/components/NewTimer'

export default {
    props: {
        timers: {
            type: Array,
            required: true
        }
    },
    methods: {
        deleteTimer(id) {
            this.$emit('delete-timer', id)
        },
        addTimer(newTimer) {
            this.$emit('add-timer', newTimer)
        },
        setActive(id) {
            this.$emit('set-active', id)
        },
        resetTimer(id) {
            this.$emit('reset', id)
        },
        unActive(id) {
            this.$emit('set-unactive', id)
        }

    },
    components: {
        Timer,
        NewTimer
    }
}
</script>
<style scoped>
    .card__container {
        display: grid;
        gap: 50px;
        justify-self: center;
        margin: 72px 0;
        align-items: stretch;
        justify-items: stretch;
        grid-template-columns: repeat(3, 225px);
    }

    @media screen and (max-width: 768px) {
        .card__container {
            grid-template-columns: repeat(2, 225px);
        }
    }

    @media screen and (max-width: 320px) {
        .card__container {
            grid-template-columns: repeat(1, 225px);
        }
    } 
</style>