<template>
    <div id="drag-file"
    @dragover.prevent 
    @dragleave.prevent 
    @dragend.prevent 
    @drop="drop">
        <p>Drag your files here</p>
    </div>
</template>

<script>
export default { 
  name: 'DragAndDropComponent',
  methods:{
    drop(e) {
        e.preventDefault();
        for (let f of e.dataTransfer.files) {
                console.log('File(s) you dragged here: ', f.path) // eslint-disable-line no-console
                
            } 
        return false;
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.drag-file {
        background-color: blue;
        color:white;
        text-align: center;
        width:300px;
        height:300px;
    }

</style>
