<script lang="ts">
	import { NewTodo } from "./classes/NewTodo.svelte";

	export let toggleModal = ():void => {};
	export let submitFormHandler;
	export let folderList: string[];

	export let isModalOpen: boolean = false;
	$: openStyle = isModalOpen ? 'flex' : 'none';

	let curr = new Date().toJSON();
 	$: date = curr.split('T')[0];

 	let tempTodo = new NewTodo(''); 
 	let folder: string = folderList[0];
 	$: {
 		console.log(folder)
 	}

</script>

<div class="modal-container" style="--display: {openStyle};">
	<form class="modal" on:submit|preventDefault={() => submitFormHandler(tempTodo, folder)}> 
		<label for="title" id="title-label">Title</label>
		<input 	type="text" 
				id="title" 
				bind:value={tempTodo.title} 
				placeholder="Do stuff..." 
				required 
				min="5" max="20">

		<label for="description" id="description-label">Description</label>
		<textarea 	cols="30" 
					rows="10" 
					name="description" 
					id="description" 
					bind:value={tempTodo.description} 
					placeholder="say something about the todo..."
					required
					min="10" max="100"></textarea>

		<label for="priority" id="priority-label">Priority</label>
		<select bind:value={tempTodo.priority} 
				name="priority" 
				id="priority" 
				required>
			<option value='high'>High</option>
			<option value='medium'>Medium</option>
			<option value='low'>Low</option>
		</select>

		<label for="folder" id="priority-label">Folder:</label>
		<select bind:value={folder} 
				name="priority" 
				id="priority" 
				required>
			
			{#each folderList as folder}
				<option value={folder}>{folder}</option>
			{/each}
		</select>

		<label for="date" id="date-label">Date</label>
		<input 	type="date" 
				name="date"
				id="date"
				bind:value={date} 
          		on:change={() => tempTodo.dueDate = new Date(date).toJSON()}
        >
        <button class="new-todo__button" on:click={toggleModal}>
        	Save
    	</button>
	</form>
</div>

<style>
	.modal-container {
		display:  var(--display);
		justify-content: center;
		align-items: center;
		position:  fixed;
		top:  0;
		left:  0;
		right: 0;
		bottom: 0;
		overflow:  hidden;
		background-color: rgba(0, 0, 0, 0.5);
		z-index: 2;
	}
	.modal {
		position: relative;
		max-width: 700px;
		max-height: 700px;
		background-color: white;
		display: flex;
		flex-direction:  column;
		padding:  10px;
		margin: 5px;
		border-radius: 5px;
	}
</style>