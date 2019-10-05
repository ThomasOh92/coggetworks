<template>
	<div class="container">
		<div id="mainboard">
			<h3>Sticky Notes</h3>
			<p>
    			<textarea placeholder="Write something awesome here..." id="new-note" rows="5"></textarea>
            </p>
            <button v-on:click="AddStickyNote">Add Note</button>
		</div>
	</div>
</template>

<script>
export default { 
  name: 'StickyNoteComponent',
  components: {
  },
  methods:{
   AddStickyNote(){
        var Mainboard = document.getElementById("mainboard");
        var NewStickyNote = document.createElement("textarea");
        NewStickyNote.setAttribute("rows", 5);
        Mainboard.appendChild(NewStickyNote)
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
