<script lang="ts">
	import type { TodoProject } from "./classes/NewProject.svelte";
import Modal from "./Modal.svelte";
	import TodoItem from "./TodoItem.svelte";

	export let currentFolderName:string;
	export let folderList;
	export let globalFolder: TodoProject[];
	$: filteredFolder = globalFolder.filter(item => currentFolderName === 'all' ? true : item.name === currentFolderName);

	const removeTodo = (folderName:string, id) => {
		const folderIndex = globalFolder.findIndex(folder => folder.name === folderName);
		const filterItems = globalFolder[folderIndex].items.filter(todo => todo.id !== id);
		globalFolder[folderIndex].items = filterItems;
		globalFolder = globalFolder;
	};

</script>

<main>
	{#each filteredFolder as folder (folder.id)}

		<h1>{folder.name}</h1>
		{#if folder.items.length}
			<ul class="todo-container">
				{#each folder.items as todo (todo.id)}
				<TodoItem {todo} {folder} {removeTodo} {folderList}/>
				{/each}
			</ul>
		{:else}
			<p>It appears that there's nothing in this folder.</p>
			<p> try to create a new todo and add it to this folder</p>
		{/if}
	{/each}
</main>

<style>
	main { 
		grid-area: main; 
		margin-left: 10px;
	}
	main ul {list-style: none;	}
	main  .todo-container {
		display: flex;
    	gap: 10px; 
    	flex-wrap: wrap;
	}

	@media screen and (min-width: 940px) {
		main {
			margin-left: 255px;
		}
	}
</style>