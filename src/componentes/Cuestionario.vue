<template>

  <section class="src-componentes-cuestionario">
    <div class="jumbotron">
      <h1>Cuestionario</h1>
      <hr>
      <hr>
      <br>
      <div v-if="preguntas.length" class="table-responsive">
      <table class="table">
        <tr>
          <th>Numero de pregunta</th>
          <th>Respuestas</th>
        </tr>
        <tr v-for="(pregunta, index) in preguntas" :key="index">
          <td>{{ pregunta.numero }} </td>
          <td>{{ pregunta.respuestas }} </td>
        </tr>
      </table>
    </div>
    </div>
  </section>

</template>

<script lang="js">

  export default  {
    name: 'src-componentes-cuestionario',
    props: [],
    mounted () {

    },
    data () {
      return {
          preguntas: [
            { numero: 1, respuestas: ['c'] },
            { numero: 2, respuestas: ['b','c'] },
            { numero: 3, respuestas: ['b','c'] },
          ],   
      }
    },
    methods: {

    },
    computed: {

    }
}


</script>

<style scoped lang="css">
  .jumbotron{
    background-color: blueviolet;
  }
  tr{
    color:white
  }
  td{
    color:white
  }
</style>
