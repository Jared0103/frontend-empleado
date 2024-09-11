<template>
  <div>
    <login-card
      @show-alert="showAlert"
    />
  </div>
</template>

<script>
import loginCard from '@/components/empleados/loginCard.vue'
export default {
  name: 'IndexPage',
  components: {
    loginCard
  },
  layout: 'login',
  methods: {
    showAlert (data) {
      this.$nuxt.$emit('show-alert', data)
    }
  }
}
</script>
