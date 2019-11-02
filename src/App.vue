<template>
  <div id="app">
    <StickyNoteComponent/>
    <hr>
    <ReferenceFilesComponent/>
    <hr>
    <VueGridComponent/>
    <hr>
    <hr>
  </div>
</template>

<script>
import VueGridComponent from './components/VueGridComponent.vue';
import ReferenceFilesComponent from './components/ReferenceFilesComponent.vue'
import StickyNoteComponent from './components/StickyNoteComponent.vue'


export default {
  name: 'app',
  components: {
    VueGridComponent,
    ReferenceFilesComponent,
    StickyNoteComponent,
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
