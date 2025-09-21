<template>
  <div class="container-fluid mt-3">
    <div class="card">
      <div class="card-header">
        <header>
          <h2>Tarea 2 de PNT2 2.1A</h2>
        </header>
      </div>


      <main>
        <!-- <Binding /> -->
        <Personas />
        
      </main>
    </div>


  </div>
</template>

<script>
import Personas from './components/Personas.vue';


export default {
    name: 'app',
    components: {
        Personas

    }
  }
</script>


<style scoped>
.card-header{
  background-color: blueviolet;
  color: white;
}
</style>
