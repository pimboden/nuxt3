<script setup lang="ts">
import { Gender, Length, Popularity } from '@/data';

interface OptionProps{
  optionData:{
    title:string;
    category:string;
    buttons: Gender[] | Popularity[] | Length[];
  };
  options:{
    gender:Gender;
    popularity:Popularity;
    length:Length;
  }
}
const props = defineProps<OptionProps>()
const getClass = (index:Number, isActive:Boolean) =>{
 var cssClasses:string[] =[]
 if(isActive)
  cssClasses.push("active")
 if(index == 0){
   cssClasses.push("left")
 }
 if(index == props.optionData.buttons.length-1){
   cssClasses.push('right')
 }
 return cssClasses.join(" ");
}
</script>
<template>
      <div class="option-container">
        <h4>{{optionData.title}}</h4>
        <div class="option-buttons">
    <button v-for="(value, index) in optionData.buttons" :key="value"
            @click="options[optionData.category] = value"
            class="option"
            :class="getClass(index, options[optionData.category] == value)"
          >      
            {{value}}
          </button>
        </div>
      </div>
</template>
<style scoped lang="scss">
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
          border-top-left-radius: 1rem;
          border-bottom-left-radius: 1rem;
        }
        &.right {
          border-top-right-radius: 1rem;
          border-bottom-right-radius: 1rem;
        }
      }
    }

</style>