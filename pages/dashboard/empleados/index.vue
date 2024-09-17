<template>
  <div style="width: 100%; padding: 0; margin: 0;">
    <v-row align="center" justify="center">
      <h1>CRUD Empleados</h1>
    </v-row>
    <v-row align="end" justify="center" style="margin-top: 10px; margin-bottom: 10px">
      <v-btn color="primary" class="ma-2" @click="crearEmpleado">
        <v-icon>mdi-account</v-icon>
        <span style="text-transform: none;">
          Crear Empleado
        </span>
      </v-btn>
    </v-row>
    <v-row align="center" justify="center">
      <v-data-table
        style="width: 100%"
        :headers="headers"
        :items="empleados"
        item-key="noempleado"
      >
        <template #[`item.acciones`]="{ item }">
          <v-tooltip bottom color="orange">
            <template #activator="{ on, attrs }">
              <v-btn
                icon
                color="warning"
                v-bind="attrs"
                :disabled="item.perfil === 'admin'"
                @click="updateEmpleado(item)"
                v-on="on"
              >
                <v-icon>mdi-update</v-icon>
              </v-btn>
            </template>
            <span>
              Actualizar al Empleado: {{ item.nombre }}
            </span>
          </v-tooltip>
          <v-tooltip bottom color="red">
            <template #activator="{ on, attrs }">
              <v-btn
                icon
                color="error"
                v-bind="attrs"
                :disabled="item.perfil === 'admin'"
                @click="deleteEmpleado(item.id)"
                v-on="on"
              >
                <v-icon>mdi-delete</v-icon>
              </v-btn>
            </template>
            <span>
              Eliminar al Empleado: {{ item.nombre }}
            </span>
          </v-tooltip>
        </template>
      </v-data-table>
    </v-row>
    <borrar-empleado
      v-if="ShowBorrar"
      :id-empleado="idEmpleado"
      @close="destruyeComponente"
      @actualiza="actualizaTabla"
    />
    <crear-empleado
      v-if="showCrear"
      @close="destruyeCrear"
      @actualiza="actualizaTabla"
    />
  </div>
</template>

<script>
import borrarEmpleado from '~/components/empleados/borrarEmpleado.vue'
import crearEmpleado from '~/components/empleados/crearEmpleado.vue'

export default {
  components: {
    borrarEmpleado,
    crearEmpleado
  },
  data () {
    return {
      empleados: [],
      headers: [
        { text: 'Nombre', align: 'center', sortable: true, value: 'nombre' },
        { text: 'Apellido Paterno', align: 'center', sortable: true, value: 'apaterno' },
        { text: 'Apellido Materno', align: 'center', sortable: true, value: 'amaterno' },
        { text: 'Correo', align: 'center', sortable: true, value: 'correo' },
        { text: 'Teléfono', align: 'center', sortable: true, value: 'telefono' },
        { text: 'Dirección', align: 'center', sortable: true, value: 'direccion' },
        { text: 'Ciudad', align: 'center', sortable: true, value: 'ciudad' },
        { text: 'Estado', align: 'center', sortable: true, value: 'estado' },
        { text: 'No. Empleado', align: 'center', sortable: true, value: 'noempleado' },
        { text: 'Perfil', align: 'center', sortable: true, value: 'perfil' },
        { text: 'Acciones', align: 'center', sortable: false, value: 'acciones' }
      ],
      ShowBorrar: false,
      idEmpleado: null,
      showCrear: false
    }
  },
  mounted () {
    this.loadEmpleados()
  },
  methods: {
    async loadEmpleados () {
      try {
        const response = await this.$axios.get('/get-all')
        if (response.data.success) {
          this.empleados = response.data.message
        } else {
          console.error('Error al cargar empleados:', response.data.message)
        }
      } catch (error) {
        console.error('Error en la solicitud:', error)
      }
    },
    deleteEmpleado (id) {
      this.idEmpleado = id
      this.ShowBorrar = true
    },
    destruyeComponente () {
      this.ShowBorrar = false
      this.idEmpleado = null
    },
    actualizaTabla () {
      this.ShowBorrar = false
      this.showCrear = false
      this.idEmpleado = null
      this.loadEmpleados()
    },
    destruyeCrear () {
      this.showCrear = false
    },
    crearEmpleado () {
      this.showCrear = true
    }
  }
}
</script>

<style scoped>
</style>
