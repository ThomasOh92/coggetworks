<template>
    <div class="container">
        <link rel="stylesheet" href="https://fonts.googleapis.com/icon?family=Material+Icons">
        <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/animate.css/3.5.2/animate.min.css">
        <grid-layout
            :layout.sync="layout"
            :col-num="parseInt(colNum)"
            :row-height="rowHeight"
            :is-draggable="draggable"
            :is-resizable="resizable"
            :is-mirrored="mirrored"
            :vertical-compact="true"
            :use-css-transforms="true"
            :responsive="responsive"
            >
            <grid-item 
                v-for="item in layout" 
                :key="item.i"
                :x="item.x"
                :y="item.y"
                :w="item.w"
                :h="item.h"
                :i="item.i"
                @resize="resize"
                @move="move"
                @resized="resized"
                @moved="moved"
                >
                    <div contenteditable="true">
                        {{item.i}}
                        <br>
                        {{item.content}}
                        <br>
                        <button @click="accessFile(item.content)">Open File!</button>
                        <button @click="removeItem(item)">Delete!</button>
                    </div>
                </grid-item>
                </grid-layout>
                <fab 
                    :position="position"
                    :position-type="positiontype"
                    :bg-color="bgColor"
                    :actions="fabActions"
                        @addItem="addItem"
                        @addStickyNote="addStickyNote"
                        ></fab>
    </div>
</template>

<script>

const { dialog } = require('electron').remote;
const fs = require('fs');
const path = require('path');
const {shell} = require('electron');


import VueGridLayout from 'vue-grid-layout';
import fab from 'vue-fab';

var testLayout = [
    {"x":0,"y":0,"w":2,"h":2,"i":"0", content: "hellothomo"}

    ];
let filename

export default {
 name: 'VueGridComponent',
 components: {
    GridLayout: VueGridLayout.GridLayout,
    GridItem: VueGridLayout.GridItem,
    fab
    },
 data()  {
            return {
                layout: JSON.parse(JSON.stringify(testLayout)),
                draggable: true,
                resizable: true,
                mirrored: false,
                responsive: true,
                rowHeight: 30,
                colNum: 12,
                index: 0,
                bgColor: '#778899',
                position: 'top-right',
                positiontype: 'absolute',
                fabActions: [
                    {
                        name: 'addItem',
                        icon: 'note_add'
                    },
                    {
                        name: 'addStickyNote',
                        icon: 'folder'
                    }
                ]
            }
        },
        mounted: function () {
            this.index = this.layout.length;
        },
        methods: {
            increaseWidth: function() {
                let width = document.getElementById("content").offsetWidth;
                width += 20;
                document.getElementById("content").style.width = width+"px";
            },
            decreaseWidth: function() {
                let width = document.getElementById("content").offsetWidth;
                width -= 20;
                document.getElementById("content").style.width = width+"px";
            },
            removeItem: function(item) {
                //console.log("### REMOVE " + item.i);
                this.layout.splice(this.layout.indexOf(item), 1);
            },
            addItem: function() {
                // let self = this;
                //console.log("### LENGTH: " + this.layout.length);
                dialog.showOpenDialog(
                    (filePath) => {
                    console.log(filePath);
                    const filopatho = String(filePath);
                    console.log(filopatho);
                    const filename = path.basename(filopatho);
                    console.log(filename)
                    fs.copyFile(filopatho,'./src/TestStuffHolder/' + filename, (err) => {if (err) throw err});
                    let item = {"x":0,"y":0,"w":2,"h":2,"i":this.index+"", content: filename};
                    this.index++;
                    this.layout.push(item);
                    } 
                )

            },
            move: function(i, newX, newY){
                ("MOVE i=" + i + ", X=" + newX + ", Y=" + newY);
            },
            resize: function(i, newH, newW, newHPx, newWPx){
                ("RESIZE i=" + i + ", H=" + newH + ", W=" + newW + ", H(px)=" + newHPx + ", W(px)=" + newWPx);
            },
            moved: function(i, newX, newY){
                ("### MOVED i=" + i + ", X=" + newX + ", Y=" + newY);
            },
            resized: function(i, newH, newW, newHPx, newWPx){
                ("### RESIZED i=" + i + ", H=" + newH + ", W=" + newW + ", H(px)=" + newHPx + ", W(px)=" + newWPx);
            },
            alert(){
                alert('Clicked on alert icon');
            },
            addStickyNote(){   
                let item = {"x":0,"y":0,"w":2,"h":2,"i":this.index+"", content: "type your notes here!"};
                this.index++;
                this.layout.push(item);
                //need to figure out how to turn this into a sticky note//
                
                /*const f = document.createElement('input');
                f.style.display='none';
                f.type='file';
                f.name='file';
                f.click();*/
            },
            accessFile(filename){
                console.log(filename + "is being opened")
                var absolutefilepath = path.resolve('./src/TestStuffHolder/')
                shell.openItem(absolutefilepath + '/'+ filename)
            }
            //Shell doesn't seem to work with relative path, find a way to convert?
            //C:\Users\ohcst\Dropbox\web-projects\Coggets - Electron\coggetsfilemanager\src\TestStuffHolder
         }
    }

</script>


<style>



.vue-grid-item {
    background: #ccc;
    border: 1px solid black;
}

.vue-grid-item .card{
  height: 100%;
  box-shadow: 0 0 4px -2px rgba(0, 0, 0, .5);
  transition: all 200ms ease
}

.vue-grid-item .button{
  background-color: #4CAF50; /* Green */
  border: none;
  color: white;
  padding: 15px 32px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
}
</style>
