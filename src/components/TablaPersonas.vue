<template>
    <div id="tabla-personas">
        <div v-if="!personas.length" class="alert alert-info" role="alert">
            no se han agregado perosnas
        </div>
        <table class="table">
            <thead>
                <tr>
                    <th>Nombre</th>
                    <th>Apellidos</th>
                    <th>Email</th>
                    <th>Acciones</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="persona in personas" :key="persona.id">
                    <td v-if="editando === persona.id">
                        <input type="text" class="form-control" v-model="persona.nombre">
                    </td>
                    <td v-else>
                        {{ persona.nombre}}
                    </td>
                    <td v-if="editando === persona.id">
                        <input type="text" class="form-control" v-model="persona.apellido">
                    </td>
                    <td v-else>
                        {{persona.apellido}}
                    </td>
                    <td v-if="editando === persona.id">
                        <input type="email" class="form-control" v-model="persona.email">
                    </td>
                    <td v-else>
                        {{persona.email}}
                    </td>
                    <td>
                        <button v-if="editando === persona.id" class="btn btn-success m-1" @click="guardarPersona(persona)">
                             💾 Guardar
                        </button>
                        <button v-else class="btn btn-danger m-1" @click="$emit('delete-persona', persona.id)">
                            🗑️ Eliminar
                        </button>
                        <button v-if="editando === persona.id" class="btn btn-danger m-1" @click="cancelarEdicion(persona)">
                             ❌ Cancelar
                        </button>
                        <button v-else class="btn btn-primary m-1" @click="editarPersona(persona)">✏️ Editar </button>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<script>
export default {
    name: 'tabla-personas',
    data(){
        return {
            editando: null
        }
    },
    props:{
        personas: Array
    },
    methods: {
        editarPersona(persona){
            this.pesonaEditada = Object.assign({}, persona)
            this.editando = persona.id
        },
        guardarPersona(persona){
            if (!persona.nombre.length || !persona.apellido.length || !persona.email.length) {
                return;  
            }
            this.$emit("actualizar-persona", persona.id, persona)
            this.editando = null
        },
        cancelarEdicion(persona){
            Object.assign(persona, this.personaEditada)
            this.editando=null
        }
    }
}
</script>

<style scoped>

</style>