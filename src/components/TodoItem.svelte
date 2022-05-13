<script lang="ts">
	import type { TodoProject } from "./classes/NewProject.svelte";
	import type { Todo } from "./classes/NewTodo.svelte";

	export let todo: Todo;
	export let folder: TodoProject;	
	export let removeTodo;

	let curr = new Date(todo.dueDate).toJSON();
 	$: date = curr.split('T')[0];

	let disabled: boolean = true;
</script>

<li>
	<input 	type="text" 
			bind:value={todo.title} 
			min="5" max="20"
			{disabled} />
	<textarea 	bind:value={todo.description} 
				min="10" max="100"
				{disabled}></textarea>
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

	<div class="todo-button__container">
		<button on:click={() => disabled = !disabled} >
			{disabled ? 'edit' : 'save'}
		</button>
		<button on:click={() => removeTodo(folder.name,todo.id)}>remove</button>
	</div>
</li>

<style>
	input, textarea, select{
		display:  block;
		resize: none;
	}

	input:disabled, textarea:disabled, select:disabled {
		background-color: white;
		color:  black;
		font-weight: 600;
		border: none;
		outline: none;
	}
</style>