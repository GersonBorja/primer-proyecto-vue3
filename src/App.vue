<script setup>

  const nombre = 'Gerson Borja'
  const frutas = ['🍌', '🍎', '🍇', '🍉']
  const styleColor = 'color: tomato'
  const arrayFrutas = [
    {
    name: "Manzana",
    price: "$1.00",
    description: "Una manzana",
    stock: 0
    },
    {
      name: "Pera",
      price: "$2.00",
      description: "Una pera",
      stock: 5
    },
    {
      name: "Naranja",
      price: "$3.00",
      description: "Una naranja",
      stock: 12
    }
  ]
  const clickme = (event) => {
    alert('ME DISTE UN CLICK' + event.target.innerText)
  }
  
  // contador
  import {ref} from 'vue'
  let counter = ref(0)
  const incrementar = () => {
    counter.value++
  }
  const decremento = () => {
    counter.value--
  }
  const resetear = () => {
    counter.value = 0
  }
  
  let computedStyle = () => {
  if (counter.value === 0) {
    return 'text-gray-400';
  } else if (counter.value > 0) {
    return 'text-green-400';
  } else if (counter.value < 0) {
    return 'text-red-400';
  }
}

const numerosFavoritos = ref([])
const agregarFavoritos = () => {
  numerosFavoritos.value.push(counter.value)
}

const validarRepetidos = () => {
  if(numerosFavoritos.value.includes(counter.value)){
    return true
  }else{
    return false
  }
}
</script>

<template>
  <h1 :style="styleColor">Bienvenido {{ nombre.toUpperCase() }}</h1>
  <ul>
    <template v-for="(fruta) in arrayFrutas" v-bind:key="fruta.name">
      <li v-if="fruta.stock >= 2"><b>{{ fruta.name }}</b> - {{ fruta.price }}</li>
    </template>
  </ul>
  <br>
  <hr>
  <br>
  <h1>Otra manera</h1>
  
  <ul>
    <li v-for="(fruta) in arrayFrutas" v-bind:key="fruta.name">
       {{ fruta.name }} - {{ fruta.stock }} <span v-if="fruta.stock <= 1" :style="styleColor">El stock es muy bajo</span>
    </li>
  </ul>
  <br>
<hr>
<br>
<h1 class="text-2xl font-bold">Eventos con Vue (click)</h1>
<a href="#clickme" v-on:click.prevent="clickme($event)">Hazme click</a>
<br>
<hr>
<br>
<h1 class="text-2xl font-bold">Reactividad en Vue (ref)</h1>
<div class="text-2xl text-bold" v-bind:class="computedStyle()">{{ counter }}</div>
<button class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded-full" v-on:click="incrementar">Incrementar contador ++</button><br><br>
<button class="bg-red-500 hover:bg-red-700 text-white font-bold py-2 px-4 rounded-full" v-on:click="decremento">Decrementar contador --</button><br><br>
<button class="bg-green-500 hover:bg-green-700 text-white font-bold py-2 px-4 rounded-full" v-on:click="resetear">Resetear contador X</button><br><br>
<button class="bg-amber-500 hover:bg-amber-700 text-white font-bold py-2 px-4 rounded-full" v-bind:disabled="validarRepetidos()" @click="agregarFavoritos">Agregar</button>
<h2 class="text-2xl mt-10">Numeros favorito</h2>
<ul>
  <li class="p-4 border-solid border-gray-100 border-b" v-for="num in numerosFavoritos"> {{ num }}</li>
</ul>
</template>
