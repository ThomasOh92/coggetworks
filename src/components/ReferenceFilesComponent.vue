<template>
    <div class="drag-file"
    @dragover.prevent 
    @dragleave.prevent 
    @dragend.prevent 
    @drop="drop">
        <p>Drag your files here</p>
    </div>
</template>

<script>
const { dialog } = require('electron').remote;
const fs = require('fs');
const path = require('path');
const {shell} = require('electron');

import { access } from 'fs';

export default { 
  name: 'ReferenceFilesComponent',
  methods:{
    drop(e) {
        e.preventDefault();
        for (let f of e.dataTransfer.files) {
                console.log('File(s) you dragged here: ', f.path) // eslint-disable-line no-console
                var NewReferenceFile =  document.createElement("img");
                NewReferenceFile.src = require('@/assets/microsoft-word.png');
                NewReferenceFile.setAttribute("width", "42");
                NewReferenceFile.setAttribute("height", "42");
                e.target.appendChild(NewReferenceFile);
                NewReferenceFile.onclick = function(){
                    var filepath = f.path;
                    shell.openItem(filepath)
                }
            } 
        return false;
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.drag-file {
        background-color: white;
        color:black;
        text-align: center;
        width:300px;
        height:300px;
    }

</style>
