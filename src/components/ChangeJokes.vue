<script setup>
import {reactive, ref} from "vue";


const joke = reactive({

  value: 'Chuck Norris doesn\'t use straws, he summons the liquid inside him.'

})

const getJoke = () => {
  fetch('https://api.chucknorris.io/jokes/random')
      .then(response => response.json())
      .then(data => {
         joke.value=data.value;
      });
}

</script>


<template>
  <div class="card" style="width:100%;">
    <h3>{{ joke.value }}</h3>
    <div class="card-body">
      <button @click="getJoke()" class="btn btn-primary">New Jokes</button>
    </div>
  </div>
</template>


<style scoped>

</style>