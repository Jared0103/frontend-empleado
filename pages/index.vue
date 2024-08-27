<template>
  <login-card />
</template>

<script>
import loginCard from '@/components/empleados/loginCard.vue'
export default {
  name: 'IndexPage',
  components: {
    loginCard
  },
  layout: 'login'
}
</script>
