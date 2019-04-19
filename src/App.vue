<template>
  <div id="app">
    <VueGridComponent/>
    <hr>
    <DragAndDropComponent/>
    <hr>
  </div>
</template>

<script>
import VueGridComponent from './components/VueGridComponent.vue';
import DragAndDropComponent from './components/DragAndDropComponent.vue'

export default {
  name: 'app',
  components: {
    VueGridComponent,
    DragAndDropComponent,
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
