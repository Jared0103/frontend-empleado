<template>
  <v-app>
    <v-main>
      <div v-if="showAlert" class="alert-overlay">
        <ui-alert :color="color" :type="type" :icon="icon" :message="message" />
      </div>
      <v-row align="center" justify="center" class="login">
        <Nuxt />
      </v-row>
    </v-main>
  </v-app>
</template>

<script>
export default {
  data () {
    return {
      showAlert: false,
      color: '',
      type: '',
      message: '',
      icon: ''
    }
  },
  created () {
    this.$nuxt.$on('show-alert', (data) => {
      console.log('🚀 ~ layout ~ data:', data)
      this.showAlert = true
      this.color = data.color
      this.type = data.type
      this.message = data.message
      this.icon = data.icon
      setTimeout(() => {
        this.showAlert = false
      }, 2000)
    })
  },
  beforeDestroy () {
    this.$nuxt.$off('show-alert')
  }
}
</script>

<style scoped>
.login {
  width: 100%;
  height: 100%;
  background-color: #FFAB91;
}

.alert-overlay {
  position: fixed;
  top: 0;
  right: 0;
  width: auto;
  display: flex;
  justify-content: flex-end;
  align-items: flex-start;
  z-index: 1000;
}

.ui-alert {
  margin: 0;
}
</style>
