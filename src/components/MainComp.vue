<script setup>
import { ref } from 'vue'
import ScenaStart from './ScenaStart.vue'
import SceneInstruction from './SceneInstruction.vue'
import SceneMain1 from './SceneMain1.vue';
import SceneMain2 from './SceneMain2.vue';
import SceneLevelOneChoise from './SceneLevelOneChoise.vue';
import SceneLevelTwoChoise from './SceneLevelTwoChoise.vue';
import SceneWin from './SceneWin.vue';
import SceneLoose from './SceneLoose.vue';

const if_plansza_poczatkowa = ref(true)
const if_instrukcja = ref(false)
const if_level_one_choise = ref(false)
const if_level_two_choise = ref(false)
const if_main1 = ref(true)
const if_main2 = ref(false)
const if_win = ref(false)
const if_loose = ref(false)


function change() {
    if_plansza_poczatkowa.value = false;
    if_instrukcja.value = true;
}

function change_instrukcja() {
    if_instrukcja.value = false
    if_level_one_choise.value = true
}

function change_level_one_choise() {
    if_level_one_choise.value = false;
    if_main1.value = true;
}

function change_level_two_choise() {
    if_level_one_choise.value = false;
    if_main2.value = true;
    console.log("wybrano poziom 2")
}

function koniec_etapu1() {


    if (if_main1.value) {
        if_main1.value = false;
        if_level_two_choise.value = true;
    } else {
        if_win.value = true;
    }
}

function loose() {
    if_loose.value = true;
}
function graj_jeszcze_raz() {
    console.log('graj_jeszcze_raz')
    if_loose.value = false;
    if_win.value = false;
    if_main1.value = false;
    if_main2.value = false;
    if_level_two_choise.value = true
}
function koniec_gry() {
    console.log('koniec_gry')
    if_loose.value = false;
    if_win.value = false;
    if_main1.value = false;
    if_main2.value = false;
    if_plansza_poczatkowa.value = true;
}
</script>



<template>
    <ScenaStart v-if="if_plansza_poczatkowa" @koniec-planszy="change()" />
    <SceneInstruction v-if="if_instrukcja" @koniec-instrukcja="change_instrukcja()" />
    <SceneLevelOneChoise v-if="if_level_one_choise" @wybor-levelu1="change_level_one_choise" />
    <SceneLevelTwoChoise v-if="if_level_two_choise" @wybor-levelu1="change_level_one_choise"
        @wybor-levelu2="change_level_two_choise" />
    <SceneMain1 v-if="if_main1" @koniec-etap1="koniec_etapu1" @przegrana="loose" />
    <SceneMain2 v-if="if_main2" @koniec-etap2="koniec_etapu1" @przegrana2="loose" />
    <SceneWin v-if="if_win" @jeszcze-raz="graj_jeszcze_raz" @koniec-gry="koniec_gry" />
    <SceneLoose v-if="if_loose" @jeszcze-raz="graj_jeszcze_raz" @koniec-gry="koniec_gry" />
</template>

<style>
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


.start:hover {
    cursor: pointer;
}
</style>