<script setup>
import { ref,onMounted,onUnmounted  } from 'vue';

const emit=defineEmits(['koniec-pulapka']);


function koniecPulapki() {
    
    // Emit the event to notify the parent component that the trap has ended
    console.log("Koniec pulapki");
}   

const if_ramka1= ref(false);


function handleKeydown(event) {
    event.preventDefault(); // Zapobiega domyślnemu zachowaniu przeglądarki, np. przeładowaniu strony przy naciśnięciu Enter
    if (event.key === 'Enter') {
        console.log('Naciśnięto Enter');
        emit('koniec-pulapka');
    }
     if (event.code === 'Tab') {
        console.log('Naciśnięto Tab');
        if_ramka1.value = true;
    }
}
onMounted(
    () => {document.addEventListener('keydown', handleKeydown)}
)


onUnmounted(() => {document.removeEventListener('keydown', handleKeydown);}          
)
</script>
<template>
    <div class="pulapka1"></div>
    <div class="ramka" v-if="if_ramka1"></div>
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
    z-index: 2;
   
}
.ramka{
    background-image: url("../assets/ramka_button.png");
    background-size:180px 80px;
    /* background-position: -3px -8px; */
    background-repeat: no-repeat;
    position: absolute;
    top: 370px;
    left: 528px;
    width: 180px;
    height: 80px;
    z-index: 1;
}
</style>