<script setup lang="ts">
import {ref} from 'vue';
import HelloWorld from './components/HelloWorld.vue'
import TheWelcome from './components/TheWelcome.vue'
const vetor = ref([{id:1, texto:"oi"}])
const id = ref (2)
function adicionar(){
  vetor.value.push({id:id.value, texto: colocar.value})
id.value++
}
const colocar = ref("")
</script>

<template>
  <header >
    <img  alt="Vue logo" class="logo" src="./assets/logo.svg" width="125" height="125" />

    <div class="wrapper">
      <HelloWorld  v-for="value in vetor" :msg=value.texto :key="value.id"/>
    </div>
  </header>
  <main>
    <input type="text" v-model="colocar">
    
    <button @click="adicionar">adicionar</button>
  </main>
</template>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
