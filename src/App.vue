<script setup>
import { ref, computed } from 'vue'
const name = "Vue dinamico";

const counter = ref(0);
const arrayfavoritos = ref([]);

const increment = () =>{
  counter.value++;
}

const discrement = () => {
  counter.value--;
}

const reset = () => {
   counter.value = 0 ;
}

const add = () => {
  arrayfavoritos.value.push(counter.value);
}
const blockBtnAdd = computed(()=>{
  const numSearch = arrayfavoritos.value.find((num)=>num === counter.value);
  return numSearch || numSearch === 0;
  
  // Otra forma
  // if(numSearch === 0) return true;
  // return numSearch ? true : false;
})

const classCounter = computed(()=>{
  if(counter.value === 0){
    return 'zero'
  }
  if(counter.value > 0){
    return 'positive'
  }
  if(counter.value < 0){
    return 'negative'
  }
})
</script>

<template>
  <div class ="container text-center mt-3">
    <h1>Hola {{name.toUpperCase()}}</h1>
    <h2 :class="classCounter">{{ counter }}</h2>
    <div class="btn-group">
      <button @click="increment" class="btn btn-success">Aumentar</button>
      <button @click="discrement" class="btn btn-danger">Disminuir</button>
      <button @click="reset" class="btn btn-secondary">Resetar boton</button>
      <button @click="add" :disabled="blockBtnAdd" class="btn btn-primary">Agregar</button>
    </div> 

    <ul class="list-group mt-4">
    <li class="list-group-item" v-for="num, index in arrayfavoritos" :key = "index">
      {{ num }}
    </li>
    </ul>
  </div>
</template>

<style>
  h1{
   color: red; 
  }
  .positive{
    color: green;
  }
  .negative{
    color: red;
  }
  .zero{
    color: peru;
  }
</style>