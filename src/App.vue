<template>
  <div class="container-fluid">
    <div class="jumbotron bg-dark">
      <h1>Examen Parcial - Baez Nicolás</h1>
      <br>
      <Navbar      />
      <router-view />
    </div>
  </div>
</template>

<script>
import Navbar from './componentes/Navbar.vue'

export default {
  name: 'App',
  components: {
    Navbar,
  }
}
</script>

<style> 
  .jumbotron{
    background-color: rgb(0, 0, 0);
  }

  h1 {
    color: white
  }
</style>
