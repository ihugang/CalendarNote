<script setup lang="ts">
import { ref } from "vue";

defineProps<{ day: number }>();

const count = ref(0);
</script>
        
<template>
    <div class="detail-cell">{{ day }}</div>
</template>
    
<style>
.detail-cell {
    display: flex;
    justify-content: center;
    align-items: center;
    align-content: center;
    width: 98%;
    min-height: 200px;
    background-color: rgb(186, 230, 252);
    cursor: pointer;
}
</style>
    