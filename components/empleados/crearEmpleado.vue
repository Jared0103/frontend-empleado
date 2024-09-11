<template>
  <v-dialog v-model="showDialog" with="800">
    <v-card>
      <v-card-title>
        Agregar Empleado
      </v-card-title>
      <v-card-text>
        Pentiente
      </v-card-text>
      <v-card-actions>
        <v-row align="center" justify="center" class="pa-2 ma-2">
          <v-btn color="green" @click="closeDialog">
            Cancelar
          </v-btn>
          |
          <v-btn color="red" @click="crearEmpleado">
            Agregar
          </v-btn>
        </v-row>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>

<script>
export default {
  data () {
    return {
      showDialog: true
    }
  },
  methods: {
    closeDialog () {
      this.showDialog = false
      this.$emit('close')
    },
    crearEmpleado () {
      // pendiente
    }
  }
}
</script>
