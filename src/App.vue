<script setup>
import { computed, ref } from 'vue';
const name = 'vue dinamico'
const styleColor = "color:blue";
const arrayColores = ["blue","red","peru"];
const activo = false;
const arrayFavoritos = ref([])
const arrayFrutas = ["🍎", "🍌", "🍉", "🍓", "🍒"];

let counter = ref(0);

 const decrementar = () =>{
    counter.value --
 }
 const reset = () => counter.value = 0; 

 const increment = () =>{
  console.log("aumentar contador");
  counter.value++;
  
 }
 const classCouter = computed(() => {
  if (counter.value === 0) {
    return 'zero'
  }
  if (counter.value > 0) {
    return 'positive'
  }
  if (counter.value < 0) {
    return 'negative'
  }
 })
 const add = () => {
  arrayFavoritos.value.push(counter.value)
 }
const arrayObjetos =[
{
            name: "Manzana",
            price: "$1.00",
            description: "Una manzana",
            stock: 3,
        },
        {
            name: "Pera",
            price: "$2.00",
            description: "Una pera",
            stock: 0,
        },
        {
            name: "Naranja",
            price: "$3.00",
            description: "Una naranja",
            stock: 20,
        },
    ];
    const objetos = {
      name: "Naranja",
            price: "$3.00",
            description: "Una naranja",
            id: 1,
    }
    // metodo - methods
    const handleClick = (message) =>{
      console.log(message)
    }
    const bloquearAdd = computed(()  =>{
      const numsearch = arrayFavoritos.value.find(num => num === counter.value)
      console.log(numsearch)
      if (numsearch === 0 ) {
        return true;
      }
      return numsearch ? true : false;
    })
</script>

<template>
  <h1>Hola con {{ name.toLocaleUpperCase() }}</h1>
  <h2> {{ arrayColores }}</h2>
  <h2 v-bind:style="styleColor">Soy un color azul</h2>
<h3 :style=" `color: ${arrayColores[2] }` ">Soy un color interpoblado</h3>

<h2>
  {{ activo ? "Estoy Activo" : "Estoy inactivo" }}
</h2>
<ul>
  <li v-for="(fruta, index) in arrayFrutas">
   {{ index }} - {{ fruta }}
  </li>
</ul>
<p v-if="activo === true">Esta terminado el video</p>
<p v-else-if="activo === false">Esta iniciando el video</p>
<p class="p2" v-else  >El video no es por iniciar sin red</p>

<h2 v-show="activo">Estoy activo con V-show</h2>
 <h3>Carrito</h3>
  <ul>
    <li v-for="(car, index) in arrayObjetos">
      {{ car.name }} posicion {{ index }}
      {{ car.price }} - {{ car.description }}
    </li>
    <li v-for="(value, propiedad, index ) in objetos" :key="value">
     {{ index }} + {{ propiedad }} - {{ value }}
    </li>
  </ul>
  <ul>
    <template v-for="item in arrayObjetos" :key="item.name">
 <li v-if="item.stock > 0">

        {{ item.name }} / {{ item.price }} - {{ item.description }}
    </li>
    </template >
   
  </ul>
  
<!--    <h2 :class="counter > 0 ? 'positive' : 'negative' ">{{ counter }} </h2> -->
  <div class="container text-center mt-3">

    <h2 :class="classCouter">{{ counter }}</h2>
    <div class="btn-group">

      <button type="submit" @click="handleClick('me diste un click')" class="btn btn-info">Activame1</button>
      <button type="submit" @click="increment" class="btn btn-success">Incrementa</button>
      <button type="submit" @click="decrementar" class="btn btn-danger">Decrementar</button>
      <button type="submit" @click="reset" class="btn btn-secondary">Resetear</button>
     <br>
     <button type="submit" @click="add" :disabled="bloquearAdd" class="btn btn-primary">Add</button>
     
    </div>
  
  <ul class="list-group mt-4">
      <li class="list-group-item" v-for="(num, index) in arrayFavoritos" 
      :key="index">
      {{ num }}</li>
    </ul>
   <button type="submit" v-on:click.rigth="handleClick('Text right')">click Right</button>
   <button type="submit" v-on:click="handleClick('Texto left')">Click left</button>
   <button type="submit" @click.middle="handleClick('Texto Middle')">Click Middle</button>
  </div>

</template>

 

<style>
 h1 {
  color: red;
 }
 p{
  color: blue;
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