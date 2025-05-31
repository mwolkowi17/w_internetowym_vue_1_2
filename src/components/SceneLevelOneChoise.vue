<script setup>
import { ref, onMounted, onUnmounted } from 'vue';
const emit=defineEmits(['wybor-levelu1']);

const if_ramka1 = ref(false);

function handleKeydown(event) {
    event.preventDefault(); // Zapobiega domyślnemu zachowaniu przeglądarki, np. przeładowaniu strony przy naciśnięciu Enter
    if (event.key === 'Enter') {
        console.log('Naciśnięto Enter');
        emit('wybor-levelu1');
    }
    if (event.code === 'Tab') {
        console.log('Naciśnięto Tab');
        if_ramka1.value = true;
    }

}

onMounted(
    () => { document.addEventListener('keydown', handleKeydown) }
)


onUnmounted(() => { document.removeEventListener('keydown', handleKeydown); }
)
</script>

<template>
    <div class="tlo-level1"></div>
    <div class="ramka" v-if="if_ramka1"></div>
    <button class="level-one-button" @click="$emit('wybor-levelu1')" role="img" alt="ikona Level 1" aria-label="Przycisk level 1" aria-disabled="false" ></button>
</template>

<style scoped>
.tlo-level1 {
    background-image: url("../assets/plansza_poziom1_wybor.png");
    background-size: 1280px 720px;
    height: 720px;
    width: 1280px;
    top: 0px;
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

.ramka {
    background-image: url("../assets/ramka_button.png");
    background-size: 550px 180px;
    /* background-position: -3px -8px; */
    background-repeat: no-repeat;
    position: absolute;
    top: 267px;
    left: 110px;
    width: 550px;
    height: 180px;
}
</style>