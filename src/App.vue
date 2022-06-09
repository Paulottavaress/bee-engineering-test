<template>
  <Header />
  <RouterView />
</template>

<script>
import Header from '@/components/Layout/Header.vue'

export default {
  components: { 
    Header,
  },
}
</script>


<style>
  * {
    font-family: 'Poppins', sans-serif;
  }
</style>
