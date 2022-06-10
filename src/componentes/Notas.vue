<template>

  <section class="src-componentes-notas">
    <div class="jumbotron">
      <h1>Notas</h1>
      <hr>
      <hr>
      <br>
      
      <vue-form :state="formState" @submit.prevent="enviarDatos()">
        
        <!--CAMPO Y VALIDACIONES-->

        <validate tag="div">
          <label for="nombre">Nombre</label>
          <input
            type="text"
            id="nombre"
            class="form-control"
            name="nombre" 
            autocomplete="off"
            v-model.trim="formData.nombre"
            required 
            :minlength="minNombreyApellido"
            :maxlength="maxNombreyApellido"
            no-espacios
          />
    
          <field-messages name="nombre" show="$dirty">
            <div slot="required"    class="alert alert-danger mt-1"> Campo requerido</div>
            <div slot="minlength"   class="alert alert-danger mt-1"> Sólo se puede ingresar como minimo {{minNombreyApellido}} caracteres</div>
            <div slot="maxlength"   class="alert alert-danger mt-1"> Sólo se puede ingresar como maximo {{maxNombreyApellido}} caracteres</div>
            <div slot="no-espacios" class="alert alert-danger mt-1"> No se pueden colocar espacios intermedios </div>
          </field-messages>
        </validate>

        <br>
        
        <!--CAMPO Y VALIDACIONES-->

        <validate tag="div">
          <label for="apellido">Apellido</label>
          <input
            type="text"
            id="apellido"
            class="form-control"
            name="apellido" 
            autocomplete="off"
            v-model.trim="formData.apellido"
            required
            :minlength="minNombreyApellido"
            :maxlength="maxNombreyApellido"
            no-espacios
          />
    
          <field-messages name="apellido" show="$dirty">
            <div slot="required"    class="alert alert-danger mt-1"> Campo requerido</div>
            <div slot="minlength"   class="alert alert-danger mt-1"> Sólo se puede ingresar como minimo {{minNombreyApellido}} caracteres</div>
            <div slot="maxlength"   class="alert alert-danger mt-1"> Sólo se puede ingresar como maximo {{maxNombreyApellido}} caracteres</div>
            <div slot="no-espacios" class="alert alert-danger mt-1"> No se pueden colocar espacios intermedios </div>
          </field-messages>
        </validate>

        <br>

        <!--CAMPO Y VALIDACIONES-->

        <validate tag="div">
          <label for="nota">Nota</label>
          <input
            type="number"
            id="nota"
            class="form-control"
            name="nota" 
            autocomplete="off"
            v-model.number="formData.nota"
            required
            :min='notaMin'
            :max="notaMax"

          />
    
          <field-messages name="nota" show="$dirty">
            <div slot="required" class="alert alert-danger mt-1">Campo requerido                       </div>
            <div slot="min"      class="alert alert-danger mt-1">nota mínima (min {{notaMin}})         </div>
            <div slot="max"      class="alert alert-danger mt-1">nota fuera de rango (max {{notaMax}}) </div>
          </field-messages>
        </validate>

        <br>
    
        <button class="btn btn-success my-3" :disabled="formState.$invalid">ENVIAR</button>
    
       </vue-form>
    
      <br>
      <label><h2>Tabla de Notas</h2></label>
      <br>

      <div v-if="alumnos.length" class="table-responsive">
        <table class="table">
          <tr>
            <th>Nombre y apellido</th>
            <th>Nota</th>
          </tr>
          <tr v-for="(alumnoRecorrido, index) in alumnos" :key="index" :style="{'background-color': analizarNota(alumnoRecorrido).color}">
            <td>{{ `${alumnoRecorrido.nombre} ${alumnoRecorrido.apellido}`}} </td>
            <td>{{  alumnoRecorrido.nota  }}</td>
          </tr>
          <tr>
            <th>PROMEDIO NOTAS</th>
          </tr>
          <tr v-for="(alumnoRecorrido, index) in alumnos" :key="index" :style="{'background-color': analizarNota(alumnoRecorrido).color}">
            <td>
              Promedio Actual:
            </td>
            <td v-if="contNotas!=0">
              {{  (acumulador / contNotas) }}
            </td>
          </tr>
        </table>
      </div>
      <h3 v-else class="alert alert-danger"> No se han ingresado Notas</h3>




    </div>
  </section>

</template>

<script lang="js">

  export default  {
    name: 'src-componentes-notas',
    props: [],
    mounted () {

    },
    data () {
      return {
        formState: {},
        formData:  this.getInitialData(),
        alumnos:   [],
        minNombreyApellido: 3,
        maxNombreyApellido: 15,
        notaMin: 0,
        notaMax: 10,
        acumulador: 0,
        contNotas: 0,
      }
    },
    methods: {
      getInitialData(){
        return {
          nombre:   null,
          apellido: null,
          nota:     null,
        }
      },
      enviarDatos(){
        let alumnoIngresado = {...this.formData}
        this.alumnos.push(alumnoIngresado)

        this.formData = this.getInitialData()
        this.formState._reset()
      },
      analizarNota(alumnoRecibido){
        let nota  = alumnoRecibido.nota
        let color = '#080'
        if(nota <= 6) color = '#FF0'
        if(nota < 4) color = '#F00'
        this.acumulador += nota
        this.contNotas++
        // console.log(this.acumulador)
        return{
          valor: nota,
          color
        }
      }
    },
    computed: {

    }
}


</script>

<style scoped lang="css">
  .jumbotron{
    background-color: blueviolet;
  }
  .table-responsive{
    background-color: white;
  }
  label{
    color: white
  }
</style>
