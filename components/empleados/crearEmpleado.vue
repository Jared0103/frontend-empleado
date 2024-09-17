<template>
  <v-dialog v-model="showDialog" with="800">
    <v-card>
      <v-card-title>
        Agregar Empleado
      </v-card-title>
      <v-card-text class="mt-4">
        <v-form ref="frmCreate">
          <v-row>
            <v-col cols="12">
              <v-text-field
                v-model="empleado.nombre"
                label="Escribe el Nombre"
                placeholder="Escribe el Nombre"
                dense
                filled
                outlined
                :rules="[regla.requerido]"
              />
            </v-col>
          </v-row>
          <v-row>
            <v-col cols="6">
              <v-text-field
                v-model="empleado.apaterno"
                label="Escribe el A. Paterno"
                placeholder="Escribe el A. Paterno"
                dense
                filled
                outlined
                :rules="[regla.requerido]"
              />
            </v-col>
            <v-col cols="6">
              <v-text-field
                v-model="empleado.amaterno"
                label="Escribe el A. Materno"
                placeholder="Escribe el A. Materno"
                dense
                filled
                outlined
              />
            </v-col>
          </v-row>
          <v-row>
            <v-col cols="12">
              <v-text-field
                v-model="empleado.direccion"
                label="Escribe la Direccion"
                placeholder="Escribe la Direccion"
                dense
                filled
                outlined
                :rules="[regla.requerido]"
              />
            </v-col>
          </v-row>
          <v-row>
            <v-col cols="4">
              <v-text-field
                v-model="empleado.telefono"
                label="Escribe el Telefono"
                placeholder="Escribe el Telefono"
                dense
                filled
                outlined
                :rules="[regla.requerido]"
              />
            </v-col>
            <v-col cols="4">
              <v-text-field
                v-model="empleado.ciudad"
                label="Escribe la Ciudad"
                placeholder="Escribe la Ciudad"
                dense
                filled
                outlined
              />
            </v-col>
            <v-col cols="4">
              <v-text-field
                v-model="empleado.estado"
                label="Escribe el Estado"
                placeholder="Escribe el Estado"
                dense
                filled
                outlined
              />
            </v-col>
          </v-row>
          <v-row>
            <v-col cols="4">
              <v-text-field
                v-model="empleado.correo"
                label="Escribe el Correo"
                placeholder="Escribe el Correo"
                dense
                filled
                outlined
                :rules="[regla.requerido, regla.correo]"
              />
            </v-col>
            <v-col cols="4">
              <v-text-field
                v-model="empleado.contrasena"
                type="password"
                label="Escribe el Password"
                placeholder="Escribe el Password"
                dense
                filled
                outlined
                :rules="[regla.requerido, regla.size]"
              />
            </v-col>
            <v-col cols="4">
              <v-combobox
                v-model="empleado.perfil"
                :items="perfiles"
                dense
                outlined
                filled
              />
            </v-col>
          </v-row>
        </v-form>
      </v-card-text>
      <v-card-actions>
        <v-row align="center" justify="center" class="pa-2 ma-2">
          <v-btn color="red" @click="closeDialog">
            Cancelar
          </v-btn>
          |
          <v-btn color="green" @click="crearEmpleado">
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
      showDialog: true,
      empleado: {},
      perfiles: ['admin', 'rh', 'conta', 'sistemas'],
      regla: {
        requerido: v => (v || '').length > 0 || 'El Campo es Requerido',
        size: v => (v || '').length > 6 || 'This field needs 6 chars',
        correo: v => /^\w+([.-]?\w+)*@\w+([.-]?\w+)*(\.\w{2,3})+$/.test(v) || 'E-mail must be valid'
      }
    }
  },
  mounted () {
    this.empleado.perfil = 'admin'
  },
  methods: {
    closeDialog () {
      this.showDialog = false
      this.$emit('close')
    },
    async crearEmpleado () {
      // pendiente
      const isValid = this.$refs.frmCreate.validate()
      if (isValid) {
        this.empleado.noempleado = new Date()
        const res = await this.$axios.post('/create', this.empleado)
        console.log('🚀 ~ res:', res)
        if (res.data.success) {
          this.$emit('actualiza')
        }
      }
    }
  }
}
</script>
