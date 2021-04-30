<template>
  <div id="app">
    <InputNote/>
  </div>
</template>

<script>
import InputNote from './components/InputNote.vue';


export default {
  name: 'App',
  components: {
    InputNote
  }
}
</script>

<style>

#app {
  width: 1440px;
  margin: 0 auto;
  padding-top: 150px;
}
</style>
