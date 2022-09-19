<script setup lang="ts">
import { ref } from "vue";
import Cell from "./Cell.vue";

defineProps<{ msg: string }>();

const month = ref(0);
const year = ref(0);
const days = ref(0);
const firstDayWeek = ref(0);
const rows = ref(0);
const selectedDay = ref(0);

// init
const init = () => {
    let today = new Date();
    month.value = today.getMonth() + 1;
    year.value = today.getFullYear();
    days.value = new Date(year.value, month.value, 0).getDate();
    firstDayWeek.value = new Date(year.value, month.value - 1, 1).getDay();
    rows.value = Math.ceil((days.value + firstDayWeek.value) / 7);
}

const isDay = (i: number) => {
    return i <= firstDayWeek.value + days.value && i > firstDayWeek.value;
}

const isWeekend = (i: number) => {
    return i % 7 == 0 || i % 7 == 1;
}

const chooseDay = (i: number) => {
    selectedDay.value = i - firstDayWeek.value;
    console.log(i + ' ' + selectedDay.value);
}

init()

</script>

<template>
    <div class="calendar">
        <h1 class="title">{{year}}年{{month}}月</h1>

        <div class="grid-row firstrow">
            <div class="grid-cell border red">日</div>
            <div class="grid-cell border">一</div>
            <div class="grid-cell border">二</div>
            <div class="grid-cell border">三</div>
            <div class="grid-cell border">四</div>
            <div class="grid-cell border">五</div>
            <div class="grid-cell border red">六</div>
            <!-- <Cell title="Hello World" /> -->
        </div>
        <div class="grid-row" v-for="n in rows" v-bind:key="n">
            <div :class="{'grid-cell':true,'border':isDay((n-1)*7+m),'selected':selectedDay==(n-1)*7+m-firstDayWeek}"
                v-for="m in 7" v-bind:key="m">
                <Cell :weekend="isWeekend((n-1)*7+m)" :day="(n-1)*7+m - firstDayWeek" v-if="isDay((n-1)*7+m)"
                    @click="chooseDay((n-1)*7+m)" />
            </div>
        </div>
    </div>
</template>
    
<style scoped>
.calendar {
    width: 98%;
    height: 100%;
    margin: 5px auto;
    background-color: rgb(186, 230, 252);
    border: 1px solid rgb(0, 0, 0);
}

h1.title {
    font-size: 32px;
    line-height: 60px;
}

.firstrow {
    font-weight: bold;
    height: 32px;
    margin-top: 10px;
}

.grid-row {
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    justify-content: space-around;
    align-items: center;
    align-content: center;
    margin: 10px auto;
}

.border {
    border: solid 1px rgba(90, 90, 90, 0.4);
}

.grid-cell {
    display: flex;
    justify-content: center;
    align-items: center;
    align-content: center;
    width: 13.8%;
    min-height: 32px;
    background-color: rgb(186, 230, 252);

}

.selected {
    border: dotted 3px rgba(2, 205, 2, 0.8);
    font-weight: bold;
}

.red {
    color: red;
}
</style>
    