<script lang="ts">
	import Fa from 'svelte-fa'
  	import { faTrashCan } from '@fortawesome/free-solid-svg-icons'

	import type { TodoProject } from "./classes/NewProject.svelte";
	import type { Todo } from "./classes/NewTodo.svelte";
	import EditModal from "./EditModal.svelte";

	export let todo: Todo;
	export let folder: TodoProject;	
	export let removeTodo;
	export let folderList;


	let curr = new Date(todo.dueDate).toJSON();
 	$: date = curr.split('T')[0];


	let isModalOpen: boolean = false;


</script>

<li class="todo-info">
	<input type=checkbox checked={todo.checked} >
	<div class="description" on:click={() => isModalOpen = true }>
		<h3><span>Title:</span> {todo.title}</h3>
		<p>{todo.description}</p>	
	</div>
	<button class="remove-button" on:click={() => removeTodo(folder.name,todo.id)}>
		<Fa icon={faTrashCan} />
	</button>

	
</li>
{#if isModalOpen}
	<EditModal bind:isModalOpen bind:todo {folderList} />
{/if}

<style>
	.todo-info {
		display: flex;
    	width: 270px;
	    justify-content: space-between;
	    align-items: center;
	    padding: 0px 15px;
	    box-shadow: rgb(60 64 67 / 30%) 0px 1px 2px 0px, rgb(60 64 67 / 15%) 0px 1px 3px 1px;
	    border-radius:  5px;
	    text-align: center;
	}
	.todo-info:hover, .todo-info:active {
    	box-shadow: rgb(60 64 67 / 30%) 0px 1px 5px 0px, rgb(60 64 67 / 15%) 0px 1px 3px 1px;
	}
	.todo-info h3 {
		margin: 5px;
	}
	.todo-info p {
		margin: 5px;
	}	
	.remove-button {
		background-color: transparent;
		outline: none;
		border: none;
	}
	.remove-button:hover {
		color: red;
	}
	.description {
		cursor: pointer;
	}
</style>
