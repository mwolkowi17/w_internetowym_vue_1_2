<script setup>
import { ref, onMounted, onUnmounted } from 'vue';
const emit=defineEmits(['wybor-levelu1','wybor-levelu2']);

const if_ramka1 = ref(false);

const if_lewa = ref(true);
const if_prawa = ref(false);

const choice=ref(1);

function handleKeydown(event) {
    event.preventDefault()
    if (event.key === 'Enter') {
        console.log('Naciśnięto Enter');
        if (choice.value === 1) {
            emit('wybor-levelu1');
        } else {
            emit('wybor-levelu2');
        }
       
    }
    if (event.code === 'Tab') {
        console.log('Naciśnięto Tab');
        if_ramka1.value = true;
        if (choice.value === 1) {
            if_lewa.value = false;
            if_prawa.value = true;
            choice.value = 2;
        } else {
            if_lewa.value = true;
            if_prawa.value = false;
            choice.value = 1;
        }
    }

}

onMounted(
    () => { document.addEventListener('keydown', handleKeydown) }
)


onUnmounted(() => { document.removeEventListener('keydown', handleKeydown); }
)

</script>
<template>
<div class="tlo-level2"></div>
   <div class="ramka" :class="{'ramka-lewa': if_lewa, 'ramka-prawa':if_prawa}" v-if="if_ramka1"></div>
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

.ramka {
    background-image: url("../assets/ramka_button.png");
    background-size: 550px 180px;
    /* background-position: -3px -8px; */
    background-repeat: no-repeat;
    position: absolute;
 
    width: 550px;
    height: 180px;
}

.ramka-lewa{
   top: 267px;
    left: 110px;
}

.ramka-prawa{
    top: 267px;
    left: 627px;
}
</style>