<script setup>

import {reactive, ref} from "vue";

const countries = reactive([
    {
      name: "Bangladesh",
      capital: "Dhaka",
     },
    {
      name: "Nepal",
      capital: "kathmundo",
     },
])

function getCountries(list='All'){
   countries.length=0;
  fetch('https://restcountries.com/v3.1/all?fields=name,capital').
  then(response=>response.json()).
  then(data=>{

    if ('All'==list){
      data.forEach(country=>{
        countries.push({
          name:country.name.common,
          capital:country.capital[0],
        })
      })
    } else{
      data.filter(c=>c.name.common.startsWith(list)).forEach(country => {
        countries.push({
          name: country.name.common,
          capital: country.capital[0]
        })
      })
    }

  })
}



</script>


<template>
  <div class="row">

    <div class="col-md-12">
      <button @click="getCountries()" type="button" class="btn btn-primary m-2">ALL</button>
      <button @click="getCountries('A')" type="button" class="btn btn-secondary m-2">A</button>
      <button  @click="getCountries('B')" type="button" class="btn btn-success m-2">B</button>
      <button  @click="getCountries('C')" type="button" class="btn btn-danger m-2">C</button>

    </div>

  </div>

  <div class="row mt-5" >
  <div class="col-md-12">
    <ul>
      <li class="list-unstyled" v-for="(country,index) in countries" :key="index">{{index+1}} . {{country.name}}={{country.capital}}</li>
    </ul>
  </div>
  </div>


</template>


<style scoped>

</style>