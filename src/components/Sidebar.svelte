<script lang="ts">

	export let folderList: string[] = [];
	export let newFolder = (folder: string): void => console.log(folder);
	export let currentFolderName: string;
	export let changeFolder;
	let toggleCreateNewFolder: boolean = true;
	let folderName:string = '';

	const newFolderSubmit = () => {
		if (toggleCreateNewFolder) {
			newFolder(folderName);
			folderName = '';
		}
	}
	
</script>



<aside>
	<ul>
		<li on:click={() => changeFolder("all") }>All Tasks</li>
		{#each folderList as folderName}
			<li class="folder-button" on:click={() => changeFolder(folderName)}>
				{folderName}
			</li>
		{/each}
	</ul>

	<form action="" on:submit|preventDefault={newFolderSubmit}>
		<input type="text" bind:value={folderName} disabled={toggleCreateNewFolder}>
		<button on:click={() =>	toggleCreateNewFolder = !toggleCreateNewFolder}>
			{toggleCreateNewFolder ? 'Add Folder' : 'Save'}
		</button>
	</form>
</aside>



<style>
	
</style>