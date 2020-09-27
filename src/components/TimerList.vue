<template>
    <div class="card__container">
        <!-- вывод списка всех таймеров -->
        <Timer 
            v-for="timer of timers"
            v-bind:key="timer.id"
            v-bind:timer="timer"
            @delete-timer="deleteTimer"
            @set-active="setActive"
            @reset="resetTimer"
            @set-unactive="unActive"
        />
        <!-- кнопка добавления нового таймера -->
        <NewTimer
            @add-timer="addTimer"
        />
    </div>
</template>

<script>
    import Timer from "@/components/Timer"
    import NewTimer from "@/components/NewTimer"

    export default {
        // получение данных о таймерах от родительского компонента
        props: {
            timers: {
                type: Array,
                required: true
            }
        },
        methods: {
            // отправка запросов родительскому компоненту на исполнение функций
            deleteTimer(id) {
                this.$emit("delete-timer", id)
            },
            addTimer(newTimer) {
                this.$emit("add-timer", newTimer)
            },
            setActive(id) {
                this.$emit("set-active", id)
            },
            resetTimer(id) {
                this.$emit("reset", id)
            },
            unActive(id) {
                this.$emit("set-unactive", id)
            }

        },
        components: {
            Timer,
            NewTimer
        }
    }
</script>

<style scoped>

    /* главный контейнер */
    .card__container {
        display: grid;
        gap: 50px;
        justify-self: center;
        margin: 72px 0;
        align-items: stretch;
        justify-items: stretch;
        grid-template-columns: repeat(3, 225px);
    }
    
    /* адаптивность */
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