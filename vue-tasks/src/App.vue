<template>
  <div id="app">
    <TasksApp/>
  </div>
</template>

<script>
import TasksApp from './components/TasksApp.vue';
export default {
  name: 'App',
  components: {
    TasksApp,
  }
}
</script>

<style>
body{
  background-color: rgb(66, 66, 66);
}
</style>
