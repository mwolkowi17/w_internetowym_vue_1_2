<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import { metodyPomocnicze } from '../lib/metody-pomocnicze';
import { PawnMaps } from '../lib/pawn-maps';
import { Traps } from "../lib/traps";
import SceneQuizz1 from './SceneQuizz1.vue';
import SceneTrap from './SceneTrap.vue';

const emit = defineEmits(['koniec-etap1', 'przegrana'])

const if_ramka1= ref(false);

// function handleKeydown(event) {
//     if (event.code === 'Space') {
//         console.log('Naciśnięto Space');
//         kostka_click()
//     }
// }

function handleKeydown(event) {
    event.preventDefault();
    if (event.key === 'Enter') {
        console.log('Naciśnięto Enter');
        kostka_click();
        if_ramka1.value = false; // ukryj ramkę
    }
     if (event.code === 'Tab') {
        console.log('Naciśnięto Tab');
        if_ramka1.value = true;
    }

}

onMounted(() => { document.addEventListener('keydown', handleKeydown); }
)

onUnmounted(() => {
    document.removeEventListener('keydown', handleKeydown);
});



//roboczo tylko dla starej funkcji
const postac1 = ref("postać")

//pozycja startowa gracza nr 1
const krok_gracz1_na_planszy = ref(0);

//zdefinowanie pozycji (mapy wszystkich pozycji) gracza nr 1
const pozycje_pionka_gracza1 = new PawnMaps().pionek_gracza1;

//początkowa ilość "szans"
const ilosc_szans = ref(3);

//widoczność przycisku Rzuć kostką
const if_rzuc_kostka = ref(true)

//widoczność kostki 
const if_widok_kostki = ref(true);

//widoczność planszy pułapka
const if_widok_pulapki = ref(false)

//widoczność planszy quizz1
const if_widok_quizz1 = ref(false);

//widoki szans na planszy

const if_szansa1 = ref(true)
const if_szansa2 = ref(true)
const if_szansa3 = ref(true)

//const obrazek_kostki = ref('../assets/kostka_1oczko.png')

let kolekcja_widoków_kostki = [
    false,
    false,
    false,
    false,
    false,
    false,
]

const isSet1 = ref(kolekcja_widoków_kostki[0])
const isSet2 = ref(kolekcja_widoków_kostki[1])
const isSet3 = ref(kolekcja_widoków_kostki[2])
const isSet4 = ref(kolekcja_widoków_kostki[3])
const isSet5 = ref(kolekcja_widoków_kostki[4])
const isSet6 = ref(kolekcja_widoków_kostki[5])

//pozycja pionka
const pionek_left = ref(20)
const pionek_top = ref(220)

const mapa_pozycji_pionka = new PawnMaps()

//flaga true/false pokazująca czy gracz nr 1 nie przeszedł całej planszy, wartość falsce wskazuje zakończenie ruchu na planszy
let kontrolka_ruch_na_planszy = true;

// licznik ruchu na planszy - faktyczny ruch pionka
let ruch_lokalny = 0;



function kostka_click() {

    if_rzuc_kostka.value = false //  ukryj przycisk rzuć kostką
    document.removeEventListener('keydown', handleKeydown);
    //========================================================================================
    let i = 0; //  set your counter to 0
    //========================================================================================
    if_widok_kostki.value = true
    console.log("rzut")
    let x = metodyPomocnicze.rzucaj();

    let wynik_rzutu = x
    console.log(x)
    for (let i = 0; i < 6; i++) {
        if (i === x) {
            kolekcja_widoków_kostki[i] = true
        }
        else {
            kolekcja_widoków_kostki[i] = false
        }


        isSet1.value = kolekcja_widoków_kostki[0]
        isSet2.value = kolekcja_widoków_kostki[1]
        isSet3.value = kolekcja_widoków_kostki[2]
        isSet4.value = kolekcja_widoków_kostki[3]
        isSet5.value = kolekcja_widoków_kostki[4]
        isSet6.value = kolekcja_widoków_kostki[5]


    }

    console.log(kolekcja_widoków_kostki)

    //!!============================ruch pionka loop =========================================
    const myLoopPionek = (arg_A, arg_B, arg_C) => {
        //  create a loop function
        setTimeout(function () {
            //  call a 1s setTimeout when the loop is called

            pionek_left.value = arg_B[arg_C.value + i][0]
            pionek_top.value = arg_B[arg_C.value + i][1]

            //console.log(arg_B)
            console.log(arg_C.value)
            console.log(arg_B[arg_C.value + i])



            //arg_A.setPosition(arg_B[arg_C + i][0], arg_B[arg_C + i][1]);

            if (ruch_lokalny >= 15) {
                console.log("Zwycięstwo!");
                kontrolka_ruch_na_planszy = false;
                console.log("wygrałeś!!!");
                wywolanie_sceny_koncowej();
            }


            ruch_lokalny++;

            i++; //  increment the counter

            if (i <= wynik_rzutu && ruch_lokalny <= 15) {
                myLoopPionek(arg_A, arg_B, arg_C); //  ..  again which will trigger another                         
            } else {
                dodanie_krokow();
                pulapka_czy_quizz();
            }


            //  ..  setTimeout()

        }, 1000);
    };


    function dodanie_krokow() {
        krok_gracz1_na_planszy.value =
            krok_gracz1_na_planszy.value + wynik_rzutu + 1;
    }


    if (kontrolka_ruch_na_planszy === true) {
        //  start the loop
        myLoopPionek(
            postac1,
            pozycje_pionka_gracza1,
            krok_gracz1_na_planszy,

        )

        console.log("krok na planszy: " + krok_gracz1_na_planszy.value);
    }

    //instancja obieku odpowiadającego za pułapki
    const trap = new Traps();

    const pulapka_czy_quizz = () => {
        console.log("sprawdzam czy pułapka albo quizz");
        console.log(i)
        console.log("wynik rzutu: " + wynik_rzutu);
        console.log("kontrolka ruch na planszy: " + kontrolka_ruch_na_planszy);
        //if (i === (wynik_rzutu+1) && kontrolka_ruch_na_planszy === true) {
        if (kontrolka_ruch_na_planszy === true) {
            console.log("pulapka albo quizz!!!");
            console.log("krok gracza na planszy: " + krok_gracz1_na_planszy.value);
            // sprawdzenie czy gracz wpadł w pułapkę
            console.log(trap.czy_polapka(krok_gracz1_na_planszy.value));
            //  tu w momencie kiedy gracz zanjdzie się na polu pułapka będzie go cofało a jak nie to odpala quizz
            if (trap.czy_polapka(krok_gracz1_na_planszy.value) === true) {
                console.log("wpadka");
                //  pokazuje planszę pułapki
                if_widok_pulapki.value = true;

            } else {
                console.log("quiz");
                if_widok_quizz1.value = true
            }
        }
    };

    const wywolanie_sceny_koncowej = () => {
        console.log("wywołanie planszy wyboru etapu nr 2");
        emit('koniec-etap1')
    };


}

const koniecPulapki = () => {
    console.log("emmiter - krok do tyłu");
    console.log(krok_gracz1_na_planszy.value);
    krok_gracz1_na_planszy.value = krok_gracz1_na_planszy.value - 2;
    ruch_lokalny = ruch_lokalny - 2;
    console.log(krok_gracz1_na_planszy.value);
    pionek_left.value = pozycje_pionka_gracza1[krok_gracz1_na_planszy.value - 1][0]
    pionek_top.value = pozycje_pionka_gracza1[krok_gracz1_na_planszy.value - 1][1]
    if_rzuc_kostka.value = true;
    document.addEventListener('keydown', handleKeydown)
}

const odejmijSzanse = () => {
    console.log("odejmij szanse");
    ilosc_szans.value = ilosc_szans.value - 1;

    console.log("ilosc_szans:" + ilosc_szans.value);

    if (ilosc_szans.value === 2) {
        if_szansa1.value = false;
    }
    if (ilosc_szans.value === 1) {
        if_szansa2.value = false;
    }
    if (ilosc_szans.value === 0) {
        if_szansa3.value = false;
        console.log("przegrałeś!!!");
        emit('przegrana');
    }
}
// roboczo dla obsługi spacji
function Spacja(){
    document.addEventListener('keydown', handleKeydown)
}

</script>
<template>
    <div class="tlo2"></div>
    <div class="pionek1" :style="{ left: pionek_left + 'px', top: pionek_top + 'px' }"></div>
    <div class="szansa1 szansa_ksztalt1" v-if="if_szansa1"></div>
    <div class="szansa2 szansa_ksztalt1" v-if="if_szansa2"></div>
    <div class="szansa3 szansa_ksztalt1" v-if="if_szansa3"></div>
    <div class="ramka" v-if="if_ramka1"></div>
    <button class="rzut1" v-if="if_rzuc_kostka" @click="kostka_click()"></button>
    <div class="kostka1" :class="{
        'kostka1image1': isSet1,
        'kostka1image2': isSet2,
        'kostka1image3': isSet3,
        'kostka1image4': isSet4,
        'kostka1image5': isSet5,
        'kostka1image6': isSet6
    }" v-if="if_widok_kostki"></div>
    <SceneTrap v-if="if_widok_pulapki" @koniec-pulapka="if_widok_pulapki = false, koniecPulapki()" />
    <SceneQuizz1 v-if="if_widok_quizz1" @koniec-quizz="if_widok_quizz1 = false, if_rzuc_kostka = true, Spacja()"
        @odejmij-szanse="odejmijSzanse" msg="Hej" :miejsceNaPlanszy="krok_gracz1_na_planszy" />
</template>
<style scoped>
.tlo2 {
    background-image: url("../assets/plansza_poziom1.png");
    background-size: 1280px 720px;
    height: 720px;
    width: 1280px;
    top: 0px;
    left: 0px;
    position: absolute;
}

.pionek1 {
    background-image: url("../assets/pionek1.png");
    background-size: 80px 80px;
    background-repeat: no-repeat;
    height: 80px;
    width: 80px;
    position: absolute;

}

.kostka1 {

    background-size: 150px 150px;
    background-repeat: no-repeat;
    left: 1041px;
    top: 467px;
    height: 150px;
    width: 150px;
    position: absolute;
    z-index: 2;
}

.kostka1image1 {
    background-image: url("../assets/kostka_1oczko.png");
}

.kostka1image2 {
    background-image: url("../assets/kostka_2oczka.png");
}

.kostka1image3 {
    background-image: url("../assets/kostka_3oczka.png");
}

.kostka1image4 {
    background-image: url("../assets/kostka_4oczka.png");
}

.kostka1image5 {
    background-image: url("../assets/kostka_5oczek.png");
}

.kostka1image6 {
    background-image: url("../assets/kostka_6oczek.png");
}

.rzut1 {
    background-image: url("../assets/rzut_przycisk.png");
    background-size: 220px 65px;
    background-repeat: no-repeat;
    top: 367px;
    left: 1000px;
    height: 67px;
    width: 220px;
    position: absolute;
    z-index: 2;
}

.rzut1:hover {
    cursor: pointer;
}

.szansa_ksztalt1 {
    background-image: url("../assets/zycie1.png");
    background-size: 67px 67px;
    background-repeat: no-repeat;

    height: 67px;
    width: 67px;
    position: absolute;
    z-index: 2;
}

.szansa1 {
    top: 267px;
    left: 980px;
}

.szansa2 {
    top: 267px;
    left: 1080px;
}

.szansa3 {
    top: 267px;
    left: 1180px;
}

.ramka{
    background-image: url("../assets/ramka_button.png");
    background-size:261px 100px;
    /* background-position: -3px -8px; */
    background-repeat: no-repeat;
    position: absolute;
    top: 350px;
    left:980px;
    width: 261px;
    height: 100px;
}
</style>
