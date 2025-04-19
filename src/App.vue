<script setup>
import { RouterView } from 'vue-router'
</script>

<script>
export default {
  name: 'app',
  components: {

  },
  data() {
    return {
    }
  }
}
</script>

<template>
  <RouterView />
</template>

<style scoped>
main {
  min-height: 100vh;
  background-color: #101010A0;
}

::-webkit-scrollbar {
  width: 5px;
}
::-webkit-scrollbar-track {
  background: #020202;
}
::-webkit-scrollbar-thumb {
  border-radius: 4px;
  background: #808080;
}
::-webkit-scrollbar-thumb:hover {
  background: #808080;
}
</style>
