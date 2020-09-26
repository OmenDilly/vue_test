<template>
    <div class='timer__card'>
        <span class='value'>{{timer.value}}</span>
        <div class='card__actions'>
            <span class='play__button material-icons'>
                play_arrow
            </span>
            <span class='stop__button material-icons'>
                stop
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
    }
}
</script>

<style scoped>
    .timer__card {
        background-color: #696969;
        color: #9E9E9E;
        font-size: 22px;
        display: grid;
        grid-template-rows: repeat(2, 60px);
    }

    .value {
        align-self: center;
        text-align: center;
    }



    .card__actions {
        display: grid;
        grid-template-columns: repeat(2, 1fr);
        gap: 48px;
        align-items: center;
        border-top: solid #9E9E9E 2px;
        /* justify-items: end; */
        /* align-self: center;
        justify-self: center; */
    }

    .card__actions span {
        cursor: pointer;
        font-size: 30px;

    }

    .card__actions span:hover {
        color: white;
    }

    .play__button {
        justify-self: end;
    }

    .stop__button {
        justify-self: start;
    }

    .active {
        border-color: white;
        color: white;
    }
</style>