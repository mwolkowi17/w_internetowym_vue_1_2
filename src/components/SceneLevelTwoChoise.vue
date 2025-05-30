<script setup>
import { ref } from 'vue';
defineEmits(['wybor-levelu1','wybor-levelu2']);
</script>
<template>
<div class="tlo-level2"></div>
   <button class="level-one-button" @click="$emit('wybor-levelu1')"></button>
   <button class="level-two-button" @click="$emit('wybor-levelu2')"></button>
</template>
<style scoped>
.tlo-level2 {
 background-image: url("../assets/plansza_poziom1_wybor.png");
    background-size: 1280px 720px;
    height: 720px;
    width: 1280px;
    top:0px;
    left: 0px;
    position: absolute;
}

.level-one-button {
   background-image: url("../assets/poziom1_button.png");
    background-size: 390px 130px;
    background-position: -2px -1px;
    position: absolute;
    top: 295px;
    left: 180px;
    width: 390px;
    height: 130px;
}
.level-one-button:hover {
    cursor: pointer;
}

.level-two-button{
    background-image: url("../assets/poziom2_button.png");
    background-size: 390px 130px;
    background-position: -2px -1px;
    position: absolute;
    top: 295px;
    left: 710px;
    width: 390px;
    height: 130px;
}

.level-two-button:hover {
    cursor: pointer;
}
</style>