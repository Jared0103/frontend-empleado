<template>
  <v-card elevation="0" color="deep-orange-lighten-1" width="400" height="300" rounded>
    <v-card-title>
      <v-row align="center" justify="center">
        <span style="color: orangered">
          Bienvenido
        </span>
      </v-row>
    </v-card-title>
    <v-card-text class="mt-4 mb-4 pt-4 pb-4">
      <v-form ref="form">
        <div class="textFields">
          <v-row style="width: 100%">
            <v-text-field v-model="usuario" :rules="size" solo />
          </v-row>
          <v-row style="width: 100%">
            <v-text-field v-model="password" :rules="size" type="password" solo />
          </v-row>
        </div>
      </v-form>
    </v-card-text>
    <v-card-actions>
      <v-row align="center" justify="center">
        <v-btn elevation="0" color="deep-orange-lighten-5" @click="loginBackend">
          <span style="text-transform: none; color:#F4511E;">
            Login
          </span>
        </v-btn>
      </v-row>
    </v-card-actions>
  </v-card>
</template>

<script>
export default {
  data () {
    return {
      usuario: '',
      password: '',
      size: [
        v => v.trim().length !== 0 || 'No puede estar vacio'
      ]
    }
  },
  methods: {
    loginBackend () {
      console.log('@@@ variables', this.usuario)
      const isValid = this.$refs.form.validate()
      if (isValid) {
        const body = {
          correo: this.usuario,
          contrasena: this.password
        }
        this.$axios.post('/login', body)
          .then((response) => {
            console.log('Login exitoso:', response.data)
          })
          .catch((error) => {
            console.error('Error en el login:', error)
          })
      } else {
        // comentario
        this.$emit('show-alert', {
          showAlert: true,
          color: 'red',
          type: 'error',
          message: 'Los datos son incorrectos',
          icon: 'mdi-error'
        })
      }
    }
  }
}
</script>

<style scoped>
.textFields {
  width: 100%;
  margin: 10px;
}
</style>
