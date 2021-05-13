<template>
  <div id="app">
    <InputNote
    @setGroup="setGroup"/>
    <div class="app__group">
      <div class="app__note">Текущие задачи: {{ index }}</div>
      <Group v-for="(data, id) in task" 
      :key="id" 
      :data="data"
      :task="task"
      @doneTask="doneTask(id)"/>
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
      index: 0,
      deleteTask: Number,
    }
  },
  mounted() {
    if (localStorage.getItem('task')) {
      try {
          this.task = JSON.parse(localStorage.getItem('task'));
          this.index = JSON.parse(localStorage.getItem('index'));
      } catch(e) {
          localStorage.removeItem('task');
      }
    }
  },
  methods: {
    setGroup(data) {
      this.task = data;
      if (this.task) {
        this.index++;
      }
      this.saveTask();
    },
    doneTask(id) {
      this.task.splice(id, 1);
      this.index--;
      if (this.index < 0) {
        this.index = 0;
      }
      this.saveTask();
    },
    saveTask() {
      const parsed = JSON.stringify(this.task);
      const parsedIndex = JSON.stringify(this.index);
      localStorage.setItem('task', parsed);
      localStorage.setItem('index', parsedIndex);
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
  width: 400px;
  margin-left: 40px;
}
.app__note {
  width: 100%;
  color: #007bff;
  font-weight: 500;
  font-size: 24px;
  display: flex;
  justify-content: center;
}
</style>
