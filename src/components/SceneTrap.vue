<script setup>
import { ref } from 'vue';

defineEmits(['koniec-pulapka']);


function koniecPulapki() {
    
    // Emit the event to notify the parent component that the trap has ended
    console.log("Koniec pulapki");
}   


</script>
<template>
    <div class="pulapka1"></div>
    <button class="przycisk_pulapka1" @click="$emit('koniec-pulapka');koniecPulapki()" ></button>
</template>
<style scoped>
.pulapka1 {
    background-image: url("../assets/zasadzka.png");
    background-size: 606px 261px;
    background-repeat: no-repeat;
    height: 261px;
    width: 606px;
    position: absolute;
    left: 320px;
    top: 220px;
}
.przycisk_pulapka1 {
    background-image: url("../assets/przycisk_dalej_imie.png");
    background-size: 150px 65px;
    background-position: -2px -5px;
    background-repeat: no-repeat;
    height: 58px;
    width: 149px;
    position: absolute;
    left: 545px;
    top: 380px;
   
}
</style>