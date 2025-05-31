<script setup>
import { ref,onMounted,onUnmounted } from 'vue'
const emit=defineEmits(['koniec-instrukcja'])

const if_ramka1= ref(false);

function handleKeydown(event) {
    event.preventDefault();
    if (event.key === 'Enter') {
        console.log('Naciśnięto Enter');
        emit('koniec-instrukcja');
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
<div class="tlo1" aria-label="Instrukcja gry"  ></div>
 <div class="ramka" v-if="if_ramka1"></div>
<button class="dalej" @click="$emit('koniec-instrukcja')" role="img" alt="ikona Dalej" aria-label="Przejdź dalej" aria-disabled="false"  ></button>
</template>
<style scoped>
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
.ramka{
    background-image: url("../assets/ramka_button.png");
    background-size:contain;
    /* background-position: -3px -8px; */
    background-repeat: no-repeat;
    position: absolute;
    top: 540px;
    left: 565px;
    width: 200px;
    height: 118px;
}
</style>