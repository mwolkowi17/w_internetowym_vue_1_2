<script setup>
import { ref,onMounted,onUnmounted } from 'vue'

const emit = defineEmits(['koniec-planszy'])

// document.addEventListener('keydown', function (event) {
//     if (event.key === 'Enter') {
//         console.log('Naciśnięto Enter');
//         emit('koniec-planszy');
//         document.removeEventListener('keydown', arguments.callee); // Usunięcie nasłuchiwania po pierwszym naciśnięciu
//     }
//     //   console.log('Naciśnięto klawisz:', event.key);
//     //   emit('koniec-planszy');
// });

const if_ramka1= ref(false);

// przykład obsługi zdarzeń z klawiatury w Vue 3
function handleKeydown(event) {
    event.preventDefault(); // Zapobiega domyślnemu zachowaniu przeglądarki, np. przeładowaniu strony przy naciśnięciu Enter
    if (event.key === 'Enter') {
        console.log('Naciśnięto Enter');
        emit('koniec-planszy');
    }
     if (event.code === 'Tab') {
        console.log('Naciśnięto Tab');
        if_ramka1.value = true;
    }

}


onMounted(
    () => {document.addEventListener('keydown', handleKeydown)}
        //   ()=>{document.addEventListener('keydown', handleTabdown);}
)


onUnmounted(() => {document.removeEventListener('keydown', handleKeydown);}
              
)
</script>

<template>
    <div class="tlo" aria-label="Plansza startowa" ></div>
    <div class="ramka" v-if="if_ramka1"></div>
    <button class="start" @click="$emit('koniec-planszy')" role="img" alt="ikona Start" aria-label="Start gry" aria-disabled="false"></button>
</template>

<style scoped>
.tytul {
    color: greenyellow;
}

.tlo {
    background-image: url("../assets/plansza_start.png");
    background-size: 1280px 720px;
    height: 720px;
    width: 1280px;
    top: 0px;
    left: 0px;
    position: absolute;
}

.start {
    background-image: url("../assets/START_przycisk.png");
    background-size: 243px 112px;
    background-position: -3px -8px;
    background-repeat: no-repeat;
    position: absolute;
    top: 400px;
    left: 500px;
    width: 240px;
    height: 100px;

}

.start:hover {
    cursor: pointer;
}

.ramka{
    background-image: url("../assets/ramka_button.png");
    background-size: 280px 118px;
    /* background-position: -3px -8px; */
    background-repeat: no-repeat;
    position: absolute;
    top: 392px;
    left: 482px;
    width: 280px;
    height: 118px;
}
</style>