<template>
  <div id="app">
    <h1 class="header">Caluclator</h1>
    <caluclator />
  </div>
</template>

<script>
import Caluclator from './components/Caluclator.vue'
export default {
  name: 'app',
  components:  {
    Caluclator
  }
}
</script>
<style scoped>
#app {
  margin-left: 30rem;
}
.header {
  margin-left: 7rem;
}
</style>
