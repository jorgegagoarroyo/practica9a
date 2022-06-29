<template>
  <img alt="Vue logo" src="./assets/logo.png">
  <h1>PERSONAS</h1>
  <formulario-persona @add-persona="agregarPersona"/>
  <tabla-personas :personas="personas" @delete-persona="eliminarPersona" @actualizar-persona="actualizarPersona"/>
</template>

<script>
import TablaPersonas from '@/components/TablaPersonas.vue'
import FormularioPersona from '@/components/FormularioPersonas.vue'

export default {
  name: 'App',
  components: {
    TablaPersonas,
    FormularioPersona
  },
  data(){
    return{ 
      personas: [
        {
          id:1,
          nombre:'Jon',
          apellido:'nieve',
          email:'jon@mail'
        },
        {
          id:2,
          nombre:'Tyrion',
          apellido:'Lannister',
          email:'tyrion@mail'
        },
        {
          id:3,
          nombre:'Daenerys',
          apellido:'Targaryen',
          email:'dae@mail'
        }
      ]
    }
  },
  methods: {
    agregarPersona(persona) {
      let id = 0;
      if(this.personas.length > 0){
        id = this.personas[this.personas.length - 1].id +1
      }
      console.log(id)
      this.personas = [...this.personas, { ...persona, id}]
    },
    eliminarPersona(id){
      console.log(id)
      this.personas = this.personas.filter(persona => persona.id !== id)
    },
    actualizarPersona(id, personaActualizada){
      this.persona = this.personas.map(persona => persona.id === id ? personaActualizada : persona)
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
