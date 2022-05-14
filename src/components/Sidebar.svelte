<script lang="ts">
	export let folderList: string[] = [];
	export let newFolder = (folder: string): void => console.log(folder);
	export let changeFolder;
	
	let toggleCreateNewFolder: boolean = true;
	let folderName:string = '';

	const newFolderSubmit = () => {
		if (toggleCreateNewFolder) {
			if (folderName && !folderList.includes(folderName)) {
				newFolder(folderName);
			}
			folderName = '';
		}
	}
</script>



<aside>
	<ul>
		<li class="folder-button_all" on:click={() => changeFolder("all") }>All Tasks</li>
		{#each folderList as folderName}
			<li class="folder-button" on:click={() => changeFolder(folderName)}>
				{folderName}
			</li>
		{/each}
	</ul>

	<form action="" on:submit|preventDefault={() => toggleCreateNewFolder && newFolderSubmit()}>
		<input 	type="text" bind:value={folderName} 
				disabled={toggleCreateNewFolder}
				required  
				min="5" max="15">
		<button on:click={() =>	toggleCreateNewFolder = !toggleCreateNewFolder}>
			{toggleCreateNewFolder ? 'Add Folder' : 'Save'}
		</button>
	</form>
</aside>



<style>
	aside { 
		width:  100%;
		height: calc(100vh - 84px);
		position: fixed;
		bottom:  0;
		border-right: 1px solid lightgrey;
		transform: translateX(var(--sidebar));
		background: white;
	}

	aside ul {
		list-style-type: none;
		margin: 0 auto;
		padding: 0;
		margin-top: 10px;
	}
	aside ul li {
    	border-radius: 5px;
    	text-align: center;
    	max-width: 180px;
    	background: white;
    	color: black;
    	font-weight: 600;
    	padding: 10px 5px;
    	margin:  auto;
    	margin-bottom: 8px;
    	box-shadow: rgb(0 0 0 / 36%) 0px 0px 1px 1px;
	}

	aside ul li:hover {
		box-shadow: rgb(0 0 0 / 20%) 0px 0px 3px 1px;
	}

	aside ul .folder-button_all {
		background: black;
    	color: white;
	}

	aside form {
		display: flex;
    	align-items: center;
    	flex-direction: column;
    	margin-top: 20px;
	}
	
	aside form input {
		max-width: 190px;
    	border-radius: 5px;
    	background-color: white;
	}

	aside form input:disabled {
    background-color: #ccc;
	}

	@media screen and (min-width: 940px) {
		aside {
			width: 245px;
			transform: translateX(0);
		}
	}


</style>