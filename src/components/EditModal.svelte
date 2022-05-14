<script lang="ts">
	import CloseButton from "./CloseButton.svelte";

	export let todo;
	export let folderList;

	export let isModalOpen: boolean = false;
	$: openStyle = isModalOpen ? 'flex' : 'none';

	let disabled = true;

	let folder: string = folderList[0];
	let curr = new Date(todo.dueDate).toJSON();
 	$: date = curr.split('T')[0];

 	const submitForm = () => disabled && (isModalOpen = false);
</script>


<div class="modal-container" style="--display: {openStyle};">
	<form action="" class="modal" on:submit|preventDefault={submitForm}>
		<CloseButton toggle={() => isModalOpen = !isModalOpen} />
		<input 	type="text" 
				bind:value={todo.title} 
				min="5" max="20"
				{disabled} />
		<textarea 	bind:value={todo.description} 
					min="10" max="100"
					{disabled}></textarea>

		<div class="priority-date__container">
		<select bind:value={todo.priority} name="priority" {disabled}>
			<option value='high'>High</option>
			<option value='medium'>Medium</option>
			<option value='low'>Low</option>
		</select>

		<input 	type="date" 
					name="date"
					id="date"
					bind:value={date}
					{disabled} 
	          		on:change={() => todo.dueDate = new Date(date).toJSON()}
	        >
	     <select bind:value={folder} 
				name="priority" 
				id="priority" 
				{disabled}
				required>
			
			{#each folderList as folder}
				<option value={folder}>{folder}</option>
			{/each}
		</select>

		<button on:click={() => disabled = !disabled} >
			{disabled ? 'edit' : 'save'}
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
	
	input:disabled, textarea:disabled, select:disabled {
		background-color: white;
		color:  black;
		font-weight: 600;
		border: none;
		outline: none;
	}
</style>