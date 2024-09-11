<template>
  <v-dialog
    v-model="showDialog"
    width="300"
    color="blue"
    persistent
  >
    <v-card>
      <v-card-title>
        Borrar Empleado
      </v-card-title>
      <v-card-text>
        ¿Estás seguro de que deseas eliminar al empleado?
      </v-card-text>
      <v-card-actions>
        <v-row align="center" justify="center" class="pa-2 ma-2">
          <v-btn color="green" @click="closeDialog">
            Cancelar
          </v-btn>
          |
          <v-btn color="red" @click="borrarEmpleado">
            Borrar
          </v-btn>
        </v-row>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>

<script>
export default {
  props: {
    idEmpleado: { type: String, default: null }
  },
  data () {
    return {
      showDialog: true
    }
  },
  mounted () {
    console.log('ID del empleado a borrar:', this.idEmpleado)
  },
  methods: {
    closeDialog () {
      this.showDialog = false
      this.$emit('close')
    },
    async borrarEmpleado () {
      try {
        const res = await this.$axios.delete(`/borrar/${this.idEmpleado}`)
        if (res.data.success) {
          this.$emit('actualiza') // Actualiza la lista de empleados
          this.closeDialog() // Cierra el diálogo después de borrar
          console.log('Empleado borrado exitosamente:', res.data.message)
        } else {
          console.error('Error al borrar el empleado:', res.data.message)
        }
      } catch (error) {
        console.error('Error en la solicitud:', error)
      }
    }
  }
}
</script>

<style scoped>
</style>
