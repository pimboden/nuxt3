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
      <div class="option-container">
        <h4>1) Choose a gender</h4>
        <div class="option-buttons">
          <button
            @click="options.gender = Gender.BOY"
            class="option left"
            :class="options.gender == Gender.BOY && 'active'"
          >
            Boy
          </button>
          <button
            @click="options.gender = Gender.UNISEX"
            class="option center"
            :class="options.gender == Gender.UNISEX && 'active'"
          >
            Unisex
          </button>
          <button
            @click="options.gender = Gender.GIRL"
            class="option right"
            :class="options.gender == Gender.GIRL && 'active'"
          >
            Girl
          </button>
        </div>
      </div>
      <div class="option-container">
        <h4>1) Choose the name's popularity</h4>
        <div class="option-buttons">
          <button
            @click="options.popularity = Popularity.TRENDY"
            class="option left"
            :class="options.popularity == Popularity.TRENDY && 'active'"
          >
            Trendy
          </button>
          <button
            @click="options.popularity = Popularity.UNIQUE"
            class="option right"
            :class="options.popularity == Popularity.UNIQUE && 'active'"
          >
            Unique
          </button>
        </div>
      </div>
      <div class="option-container">
        <h4>1) Choose name's length</h4>
        <div class="option-buttons">
          <button
            @click="options.length = Length.LONG"
            class="option left"
            :class="options.length == Length.LONG && 'active'"
          >
            Long
          </button>
          <button
            @click="options.length = Length.ALL"
            class="option center"
            :class="options.length == Length.ALL && 'active'"
          >
            All
          </button>
          <button
            @click="options.length = Length.SHORT"
            class="option right"
            :class="options.length == Length.SHORT && 'active'"
          >
            Short
          </button>
        </div>
      </div>
      <button class="primary" @click="findNames">Find Names</button>
    </div>
    <div class="cards-container">
      <div class="card" v-for="name in selectedNames" :key="name">
      <h4>{{name}}</h4>
      <p>x</p>
      </div>
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
    .option-container {
      margin-bottom: 2rem;
      .option {
        background-color: white;
        outline: 0.15rem solid rgb(249, 87, 89);
        border: none;
        padding: 0.75rem;
        width: 12rem;
        font-size: 1rem;
        color: rgb(27, 60, 138);
        cursor: pointer;
        font-weight: 200;
        &.active {
          background-color: rgb(249, 87, 89);
          color: white;
        }
        &.left {
          border-radius: 1rem 0 0 1rem;
        }
        &.right {
          border-radius: 0 1rem 1rem 0;
        }
      }
    }
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
    .card{
      background-color: rgb(27, 60, 138);
      width: 28%;
      color: white;
      border-radius: 1rem;
      padding: 0.1rem;
      margin-right: 0.5rem;
      margin-bottom: 1rem;
      position: relative;
      p{
        position: absolute;
        top:-29%;
        left: 92.5%;
        cursor: pointer;
        color: rgba(255,255,255, 0.178);
      }
    }
  }
}
</style>
