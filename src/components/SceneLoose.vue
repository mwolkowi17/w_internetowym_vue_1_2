<script setup>
import { ref } from 'vue';
defineEmits(['jeszcze-raz','koniec-gry']);
</script>

<template>
    <div class="plansza-lose"></div>
    <button class="gram-jeszcze-1" @click="$emit('jeszcze-raz')"></button>
    <button class="zakoncz-gre" @click="$emit('koniec-gry')"></button>
</template>

<style scoped>
.plansza-lose {
    background-image: url("../assets/przegrana_plansza.png");
    background-size: 1280px 720px;
    height: 720px;
    width: 1280px;
    top: 0px;
    left: 0px;
    position: absolute;
    z-index: 2;
}
.gram-jeszcze-1{
    background-image: url("../assets/gram_jeszcze_raz_button.png");
    background-size: 265px 98px;
    background-position: -1px -2px;
    position: absolute;
    top: 450px;
    left: 280px;
    width: 265px;
    height: 96px;
    z-index: 3;
}
.zakoncz-gre{
    background-image: url("../assets/zakoncz_gre_button.png");
    background-size: 265px 98px;
    background-position: -1px -2px;
    position: absolute;
    top: 450px;
    left: 720px;
    width: 265px;
    height: 96px;
    z-index: 3;
}
</style>