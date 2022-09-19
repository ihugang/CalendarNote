<script setup lang="ts">
import { ref } from "vue";

defineProps<{ day: number }>();

const count = ref(0);
</script>
        
<template>
    <div class="cell">{{ day }}</div>
</template>
    
<style>
.cell {
    display: flex;
    justify-content: center;
    align-items: center;
    align-content: center;
    width: 98%;
    min-height: 100px;
    background-color: rgb(186, 230, 252);
    cursor: pointer;
}
</style>
    