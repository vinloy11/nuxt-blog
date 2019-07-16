<template>
  <div>
    <Navbar />
    <div class="container">
      <nuxt class="main" />
    </div>
  </div>
</template>

<script>
  import Navbar from '@/components/Navbar'
  export default {
    components: {
      Navbar
    }
  }

</script>

<style>
  .main {
    margin-top: 90px;
  }
</style>
