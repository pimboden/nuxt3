<script setup lang="ts">
import { reactive, ref } from 'vue';
import { Gender, Length, Popularity, names } from '@/data';
import { isPromise } from 'util/types';

interface OptionState {
  gender: Gender;
  popularity: Popularity;
  length: Length;
}

const options = reactive<OptionState>({
  gender: Gender.BOY,
  popularity: Popularity.UNIQUE,
  length: Length.SHORT,
});
const optionsData =[
  {
    title:"1) Choose a gender",
    category:"gender",
    buttons:[
      Gender.BOY,
      Gender.UNISEX,
      Gender.GIRL,
    ]
  },{
    title:"2) Choose the name's popularity",
    category:"popularity",
    buttons:[
      Popularity.TRENDY,
      Popularity.UNIQUE
    ]
  },{
    title:"3) Choose name's length",
    category:"length",
    buttons:[
      Length.SHORT,
      Length.ALL,
      Length.LONG,
    ]
  }
]
const selectedNames = ref<string[]>([])
const findNames = () =>{
  const filteredNames = names.filter((x) => x.gender == options.gender && x.popularity == options.popularity && ( options.length ==Length.ALL ||  x.length == options.length))
  selectedNames.value = filteredNames.map(x => x.name);
}
</script>

<template>
  <div class="container">
    <h1>Bay Name Generator</h1>
    <p>Choose your options and click the "Finde names" button below</p>
    <div class="options-container">
      <option-container v-for="optionData in optionsData" :key="optionData.category" :option-data="optionData" :options="options"></option-container>
      <button class="primary" @click="findNames">Find Names</button>
    </div>
    <div class="cards-container">
      <cards-name v-for="name in selectedNames" :key="name" :name="name"></cards-name>
    </div>
    {{selectedNames}}
  </div>
</template>

<style scoped lang="scss">
.container {
  font-family: Arial, Helvetica, sans-serif;
  color: rgb(27, 60, 138);
  max-width: 50rem;
  margin: 0 auto;
  text-align: center;
  h1 {
    font-size: 3rem;
  }
  .options-container {
    background-color: rgb(255, 238, 236);
    border-radius: 1rem;
    padding: 2rem;
    width: 95%;
    margin: 0 auto;
    margin-top: 4rem;
    position: relative;
    button.primary{ 
      background-color: rgb(249, 87, 89);
      color:white;
      border: none;
      border-radius:6.5rem;
      padding: 0.75rem 4rem;
      margin-top: 1rem;
      cursor: pointer;
    }
  }
  .cards-container{
    display: flex;
    margin-top: 3rem;
    flex-wrap: wrap;

  }
}
</style>
