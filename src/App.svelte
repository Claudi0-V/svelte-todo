<script lang="ts">
	import { onMount } from 'svelte';
	import Sidebar from "./components/Sidebar.svelte";
	import Header from "./components/Header.svelte";
	import Main from "./components/Main.svelte";
	import { Project, TodoProject } from "./components/classes/NewProject.svelte";


	let globalFolder: TodoProject[] = JSON.parse(localStorage.getItem('globalFolder')) || [];

	$: {
		localStorage.setItem('globalFolder', JSON.stringify(globalFolder));
	}

	$: folderList = globalFolder.map(folder => folder.name);

	let currentFolderName: string = 'all';

	const newFolder = (folderName: string): void =>  {
		const newFolder = new Project(folderName);
		globalFolder = [...globalFolder, newFolder];
	}

	const changeFolder = (folderName: string) => currentFolderName = folderName;
	let sidebar = false;



</script>

<div id="root" class="container" style="--sidebar: {sidebar ? '0': '-100%'};">
	<Header bind:globalFolder {folderList} bind:sidebar/>
	<Sidebar {folderList} {newFolder} {currentFolderName} {changeFolder}/>
	<Main bind:globalFolder  {currentFolderName} {folderList} />
</div>

<style>
	.container {  display: grid;
  grid-template-columns: 245px 1fr 1fr;
  grid-template-rows: 75px 2.2fr 0.4fr;
  gap: 0px 0px;
  grid-auto-flow: row;
  grid-template-areas:
    "header header header"
    "main main main"
    "footer footer footer";
}
.footer { grid-area: footer; }
	
</style>
