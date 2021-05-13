<template>
  <div id="app">
    <InputNote
    @setGroup="setGroup"/>
    <Group :task="task"/>
  </div>
</template>

<script>
import InputNote from './components/InputNote';
import Group from './components/Group';


export default {
  name: 'App',
  components: {
    InputNote,
    Group
  },
  data() {
    window.onblur = function () {
      console.log('No active');
    }
    window.onfocus = function () {
      console.log('active');
    }
    return {
      task: {},
    }
  },
  methods: {
    setGroup(data) {
      this.task = data;
    },
  }
}
</script>

<style>

#app {
  width: 1070px;
  margin: 0 auto;
  padding: 50px 0;
  display: flex;
}
</style>
