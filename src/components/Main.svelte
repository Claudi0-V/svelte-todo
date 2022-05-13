<script lang="ts">
	import type { TodoProject } from "./classes/NewProject.svelte";
	import TodoItem from "./TodoItem.svelte";

	export let currentFolderName:string;
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
		<ul>
			{#each folder.items as todo (todo.id)}
			<TodoItem {todo} {folder} {removeTodo}/>
			{/each}
		</ul>
	{/each}
</main>
