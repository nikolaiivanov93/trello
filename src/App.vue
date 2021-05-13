<template>
  <div id="app">
    <InputNote
    @setGroup="setGroup"/>
    <div class="app__group">
      <Group v-for="(data, index) in task" 
      :key="index" 
      :data="data"
      :index="index"
      :task="task"
      @doneTask="doneTask(index)"/>
    </div>
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
      task: [],
      deleteTask: Number,
    }
  },
  methods: {
    setGroup(data) {
      this.task = data;
    },
    doneTask(index) {
      this.task.splice(index, 1);

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
.app__group {
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>
