<script lang="ts">
	import { TodoProject, Project } from './classes/NewProject.svelte'

	export let globalFolder: TodoProject[];
	export let onFolderChange: (folder: string) => void;
	let toggleCreateNewFolder: boolean = true;
	let folderName: string = '';

	const newFolderHandler = (): void => {
		if (!toggleCreateNewFolder) return
		const project = new Project(folderName);
		globalFolder = [...globalFolder, project]
		folderName = '';
	}
</script>

<aside>
<ul>
	<li on:click={() => onFolderChange("all")}>All Tasks</li>
	{#each globalFolder as {name}}
		<li class="folder-button" on:click={() => onFolderChange(name)}>
			{name}
		</li>
	{/each}
</ul>

<form action="" on:submit|preventDefault={newFolderHandler}>
	<input type="text" bind:value={folderName} disabled={toggleCreateNewFolder}>
	<button on:click={() =>	toggleCreateNewFolder = !toggleCreateNewFolder}>
		{toggleCreateNewFolder ? 'Add Folder' : 'Save'}
	</button>
</form>
</aside>


<style>
	
</style>