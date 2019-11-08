<template>
  <div id="app">
      <div class="column">
         <WorkingDraftComponent/>
      </div>
      <div class="column">    
        <ReferenceFilesComponent/>
      </div>
      <div class="column">
         <StickyNoteComponent/>
      </div>
  </div>
</template>

<script>
import WorkingDraftComponent from './components/WorkingDraftComponent.vue';
import VueGridComponent from './components/VueGridComponent.vue';
import ReferenceFilesComponent from './components/ReferenceFilesComponent.vue'
import StickyNoteComponent from './components/StickyNoteComponent.vue'


export default {
  name: 'app',
  components: {
    WorkingDraftComponent,
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

.column {
  float: left;
  border-right: 1px solid #000;
  padding: 10px
}
</style>
