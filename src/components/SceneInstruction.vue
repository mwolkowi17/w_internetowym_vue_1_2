<script setup>
import { ref } from 'vue'
defineEmits(['koniec-instrukcja'])

</script>
<template>
<div class="tlo1"  ></div>
<button class="dalej" @click="$emit('koniec-instrukcja')"  ></button>
</template>
<style>
.tlo1{
    background-image: url("../assets/plansza_zasady_gry.png");
    background-size: 1280px 720px;
    height: 720px;
    width: 1280px;
    top:0px;
    left: 0px;
    position: absolute;
}
.dalej{
    background-image: url("../assets/przycisk_dalej_imie.png");
    background-size: 170px 75px;
    background-position: -1px -5px;
    position: absolute;
    top: 550px;
    left: 580px;
    width: 171px;
    height: 68px;
}
.dalej:hover{
    cursor: pointer;
}
</style>
