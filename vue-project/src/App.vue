<script setup lang="ts">
import { ref, computed, onMounted, watch } from 'vue';
import { defineComponent } from 'vue';
import { RouterLink, RouterView } from 'vue-router';

function abbr(value: number): string {
  if (value >= 1_000_000) {
    return Math.floor(value / 1_000_000) + 'mil';
  } else if (value >= 1_000) {
    return Math.floor(value / 1_000) + 'k';
  } else {
    return value.toString();
  }
}

function pridatCookies(hodnoty: any[]): void{
  let array = hodnoty.slice();
  for(let i=0; i<array.length; i++){
    if(i%2==0){
      if(i == array.length-1)
      {
        let _i = i;
        _i -= _i%2;
        _i /= 2;
        let cook = array[_i*2];
        for(let j = 0; j < _i; j++){
          cook *= cookies.value;
        }
        cookies.value += cook;
      }else{
        let _i = i;
        _i -= _i%2;
        _i /= 2;
        let cook = array[_i*2] * array[_i*2+1];
        for(let j = 0; j < _i; j++){
          cook *= cookies.value;
        }
        cookies.value += cook;
      }
    }
  }
  return;
}

function cenaZvysenie(cena: number,hodnoty: any[]): number[]{
  let array = hodnoty.slice();
  let answer = 0;
  for(let i = 0; i < array.length; i++){
    answer += hodnoty[i]*cena*Math.pow(cena,i)
  }


  return [answer];
}

let cookies = ref(0);
let formattedCookies = computed(() => abbr(Math.round(cookies.value)));
let interval = setInterval(intervalFunc,1000);
pridatCookies([0,1]);
  
let itemPriceUp = ref([ 
  
]); 
let itemPriceNow = ref([2]);
let itemLevel = [];
let itemFormattedPrice = [];

let startery = ref([
  [1,1],//za click
  [0,1],//za sekundu
  [0,1]//pri nakupe
]);

function add() {pridatCookies(startery.value[0])}
function intervalFunc() {pridatCookies(startery.value[1])}//kazdu sekundu
function nakup(index:number) {
  pridatCookies(startery.value[2]);
  let cena = cenaZvysenie(itemPriceNow.value[index],itemPriceUp.value[index]);
  itemPriceNow.value[index] += cena[0];
  //pokracuj
}

//
const formattedPrice1 = computed(() => abbr(Math.round(item1Price.value)));
const formattedPrice2 = computed(() => abbr(Math.round(item2Price.value)));
const formattedPrice3 = computed(() => abbr(Math.round(item3Price.value)));
const formattedPrice4 = computed(() => abbr(Math.round(item4Price.value)));
const formattedPrice5 = computed(() => abbr(Math.round(item5Price.value)));
const formattedPrice6 = computed(() => abbr(Math.round(item6Price.value)));
const formattedPrice7 = computed(() => abbr(Math.round(item7Price.value)));

const maxLevel = ref(10);

const item1Count = ref(0);
const item1Price = ref(100);
const item1PriceChange = ref(20);

const item2Count = ref(0);
const item2Price = ref(800);
const item2PriceChange = ref(150);
const item2AddChange = ref(1);
const isItem2Active = ref(false);

const item3Count = ref(0);
const item3Price = ref(5000);
const item3PriceChange = ref(400);
const item3AddChange = ref(500);
const isItem3Active = ref(false);

const item4Count = ref(0);
const item4Price = ref(8000);
const item4PriceChange = ref(7000);

const item5Count = ref(0);
const item5Price = ref(5000);
const item5PriceChange = ref(400);

const item6Count = ref(0);
const item6Price = ref(70000);
const item6PriceChange = ref(400);

const item7Count = ref(0);
const item7Price = ref(150000);
const item7PriceChange = ref(1000);

//works
const showItem1Stats = ref(false); 
let nazvy;


function item1() {
  if (cookies.value >= item1Price.value && item1Count.value <= maxLevel.value) {
    pridatCookies(startery.value[2]);
    startery.value[0][0]++;
    cookies.value -= item1Price.value;
    item1Count.value++;
    item1Price.value += item1PriceChange.value;
    item1PriceChange.value *= 2;
  }
}

function item2() {
  if (cookies.value >= item2Price.value && item2Count.value <= maxLevel.value) {
    pridatCookies(startery.value[2]);
    cookies.value -= item2Price.value;
    item2Count.value++;
    item2Price.value += item2PriceChange.value;
    item2PriceChange.value *= 2;

    if (item2Count.value > 1) {
      item2AddChange.value *= 2;
    }
    
    startery.value[1][0]++;
  }
}

function item3() {
  if (cookies.value >= item3Price.value && item3Count.value <= maxLevel.value) {
    pridatCookies(startery.value[2]);
    cookies.value -= item3Price.value;
    item3Count.value++;
    item3Price.value += item3PriceChange.value;
    item3PriceChange.value *= 2;

    if (item3Count.value > 0) {
      item3AddChange.value *= 2;
    }

    startery.value[1][0]+=100;
  }
}

function item4() {
  if (cookies.value >= item4Price.value && item4Count.value <= maxLevel.value) {
    pridatCookies(startery.value[2]);
    cookies.value -= item4Price.value;
    item4Count.value++;
    item4Price.value += item4PriceChange.value;
    item4PriceChange.value *= 2;

    startery.value[0][1]+=0.5;
  }
}

function item5() {
  if (cookies.value >= item5Price.value && item5Count.value <= maxLevel.value) {
    pridatCookies(startery.value[2]);
    cookies.value -= item5Price.value;
    item5Count.value++;
    item5Price.value += item5PriceChange.value;
    item5PriceChange.value *= 2;

    startery.value[1][1]+=0.2;
  }
}

function item6() {
  if (cookies.value >= item6Price.value && item6Count.value <= maxLevel.value) {
    pridatCookies(startery.value[2]);
    cookies.value -= item6Price.value;
    item6Count.value++;
    item6Price.value += item6PriceChange.value;
    item6PriceChange.value *= 2;

    maxLevel.value += 10;
  }
}

function item7() {
  if (cookies.value >= item7Price.value && item7Count.value <= maxLevel.value) {
    pridatCookies(startery.value[2]);
    cookies.value -= item7Price.value;
    item7Count.value++;
    item7Price.value += item7PriceChange.value;
    item7PriceChange.value *= 2;

    startery.value[2][0] += 500;
    startery.value[2][1] += 9;
  }
}

const item1DisplayCount = computed(() => {
  return item1Count.value > maxLevel.value ? 'max' : item1Count.value;
});

const item2DisplayCount = computed(() => {
  return item2Count.value > maxLevel.value ? 'max' : item2Count.value;
});

const item3DisplayCount = computed(() => {
  return item3Count.value > maxLevel.value ? 'max' : item3Count.value;
});

const item4DisplayCount = computed(() => {
  return item4Count.value > maxLevel.value ? 'max' : item4Count.value;
});

const item5DisplayCount = computed(() => {
  return item5Count.value > maxLevel.value ? 'max' : item5Count.value;
});

const item6DisplayCount = computed(() => {
  return item6Count.value > maxLevel.value ? 'max' : item6Count.value;
});

const item7DisplayCount = computed(() => {
  return item7Count.value > maxLevel.value ? 'max' : item7Count.value;
});


// Local storage na ukladanie progresu a ekšly to funguje
/*
function saveGameState() {
  const gameState = {
    cookies: cookies.value,
    item1Count: item1Count.value,
    item2Count: item2Count.value,
    item3Count: item3Count.value,
    item4Count: item4Count.value,
    item5Count: item5Count.value,
    item6Count: item6Count.value,
    // Add other relevant game state properties as needed
  };

  localStorage.setItem('cookieClickerGameState', JSON.stringify(gameState));
}


watch(cookies, saveGameState);
watch(item1Count, saveGameState);
watch(item2Count, saveGameState);
watch(item3Count, saveGameState);
watch(item4Count, saveGameState);
watch(item5Count, saveGameState);
watch(item6Count, saveGameState);
// Repeat for other watched properties


function loadGameState() {
  const savedState = localStorage.getItem('cookieClickerGameState');
  if (savedState) {
    const parsedState = JSON.parse(savedState);
    cookies.value = parsedState.cookies;
    item1Count.value = parsedState.item1Count;
    item2Count.value = parsedState.item2Count;
    item3Count.value = parsedState.item3Count;
    item4Count.value = parsedState.item4Count;
    item5Count.value = parsedState.item5Count;
    item6Count.value = parsedState.item6Count;
    // Update other relevant properties as needed
  }
}

onMounted(loadGameState); // Load state when the component mounts
*/
</script>

<template>
<main class="body">
  <div class="menu">  
    <button
      class="item"
      @click="item1"
      @mouseover="showItem1Stats = true"
      @mouseleave="showItem1Stats = false"
    >
      Cursor Upgrade
      <div v-if="showItem1Stats" class="item-stats">
        <p>Adds 1 cookie to your click</p>
        <p>Price: {{ formattedPrice1 }}</p>
        <p>Level: {{ item1DisplayCount }}</p>
      </div>
    </button>

    <button
      class="item"
      @click="item2"
      @mouseover="showItem1Stats = true"
      @mouseleave="showItem1Stats = false"
    >
      Autoclicker
      <div v-if="showItem1Stats" class="item-stats">
        <p>Generates 1 cookie every second</p>
        <p>Price: {{ formattedPrice2 }}</p>
        <p>Level: {{ item2DisplayCount }}</p>
      </div>
    </button>

    <button
      class="item"
      @click="item3"
      @mouseover="showItem1Stats = true"
      @mouseleave="showItem1Stats = false"
    >
      Cookie Farm
      <div v-if="showItem1Stats" class="item-stats">
        <p>Generates 500 cookies every 5 seconds</p>
        <p>Price: {{ formattedPrice3 }}</p>
        <p>Level: {{ item3DisplayCount }}</p>
      </div>
    </button>

    <button
      class="item"
      @click="item4"
      @mouseover="showItem1Stats = true"
      @mouseleave="showItem1Stats = false"
    >
      Cursor <br> Multiplier
      <div v-if="showItem1Stats" class="item-stats">
        <p>50% Upgrade For Cursor</p>
        <p>Price: {{ formattedPrice4 }}</p>
        <p>Level: {{ item4DisplayCount }}</p>
      </div>
    </button>
 
    <button
      class="item"
      @click="item5"
      @mouseover="showItem1Stats = true"
      @mouseleave="showItem1Stats = false"
    >
      Autoclicker <br> Multiplier
      <div v-if="showItem1Stats" class="item-stats">
        <p>20% Upgrade For Autoclicker</p>
        <p>Price: {{ formattedPrice5 }}</p>
        <p>Level: {{ item5DisplayCount }}</p>
      </div>
    </button>

    <button
      class="item"
      @click="item6"
      @mouseover="showItem1Stats = true"
      @mouseleave="showItem1Stats = false"
    >
      Max Level <br> Upgrade
      <div v-if="showItem1Stats" class="item-stats">
        <p>+10 Levels For Every Item</p>
        <p>Price: {{ formattedPrice6 }}</p>
        <p>Level: {{ item6DisplayCount }}</p>
      </div>
    </button>

    <button
      class="item"
      @click="item7"
      @mouseover="showItem1Stats = true"
      @mouseleave="showItem1Stats = false"
    >
      Nutella Roblox <br> Upgrade 
      <div v-if="showItem1Stats" class="item-stats">
        <p>U get money $$ for every purchase</p>
        <p>Price: {{ formattedPrice7 }}</p>
        <p>Level: {{ item7DisplayCount }}</p>
      </div>
    </button>

    <div class="count">
      <h1>Cookies: <br> {{ formattedCookies }}</h1>
    </div>
</div>

<div class="cookie">
<button class="cookieB" @click="add"><img src="./assets/cookie.png" class="cookieimg"></button>
</div>
</main>

<RouterView />
</template>

<style scoped>
.body {
  background-image: url(./assets/background.png);
  background-size: cover; 
  height: 56.3rem;
}

.menu{
  padding-left: 2%;
  display: flex;
  flex-direction: row;
  align-items: center;
  width: 98.5%;
  height: 18rem;
  overflow: hidden;
  margin-top: -6%;  
}

.count{
  padding-top: 5%;
  padding-left: 1%;
  display: flex;
  justify-content: center;
  background-color: #80C4E9;
  color: #000000;
  height: 10rem;
  width: 25rem;
  border: 4px solid #000000;
  border-radius: 0px 0px 0px 40px;
  margin-top: -3%;
  position: relative;
  margin-right: 0.5%;
  font-weight: bolder;
}

.item{
  margin: 1%;
  height: 6rem;
  width: 15rem;
  position: relative;
  border: 4px solid #000000;
  background-color: #80C4E9;
  color: rgb(0, 0, 0);
  border-radius: 10px;
  font-weight: bolder;
  font-size: large;
}

.item-stats{   
  position: absolute;
  top: -4%;
  left: -3%;
  background-color: #80C4E9;
  border: 4px solid #000000;
  border-radius: 10px;
  padding: 10px;
  display: none;
  width: 86.5%;
  color: #000000;
  font-weight: bold;
  font-size: medium;
}

.item:hover .item-stats {
  display: block; 
}

.cookie {
  display: flex;
  justify-content: center;
  margin-top: 2%;
}

.cookieB {
  height: 35rem;
  width: 35rem;
  overflow: hidden;
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: transparent;
  border: none;
  max-width: 100%; 
}

.cookieimg{
  height: 42rem;
  width: auto;
  border-radius: 2000px;
  object-fit: contain;
  margin-top: -18%;
}

.cookieimg:hover{
  height: 45rem;
}
</style>