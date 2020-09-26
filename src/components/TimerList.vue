<template>
    <div class='card__container'>
        <Timer 
            v-for='timer of timers'
            v-bind:key='timer.id'
            v-bind:timer="timer"
        />
        <span class='add__button material-icons'>
            add
        </span>
    </div>

</template>

<script>
import Timer from '@/components/Timer'
export default {
    props: {
        timers: {
            type: Array,
            required: true
        }
    },
    components: {
        Timer
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
        /* grid-template-columns: repeat(auto-fill, 225px); */

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
  
    .add__button {
        background-color: #696969;
        color: #9E9E9E;
        font-size: 30px;
        display: grid;
        cursor: pointer;
        align-items: center;
        justify-items: center;
        min-height: 120px;
        min-width: 225px;
    }

    .add__button:hover {
        background-color: #9E9E9E;
        color: white;
    }

</style>