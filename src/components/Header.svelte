<script lang="ts">
	import Fa from 'svelte-fa'
  	import { faTableList } from '@fortawesome/free-solid-svg-icons'
	import type { TodoProject } from './classes/NewProject.svelte';
	import type { Todo } from './classes/NewTodo.svelte';
	import Modal from './Modal.svelte'

	export let sidebar: boolean;
	export let globalFolder: TodoProject[];
	export let folderList: string[];
	let isModalOpen: boolean = false;
	
	const toggleModal = ():void => {isModalOpen = !isModalOpen};
	const submitFormHandler = (todo: Todo, folderName: string): void => {
		const folderIndex = globalFolder.findIndex(folder => folder.name === folderName);
		globalFolder[folderIndex].items.push(todo);
		globalFolder = globalFolder;
	}
</script>

<header>
	<div class="left-header">
		<span class="fa-icon" on:click={() => sidebar = !sidebar}>
			<Fa icon={faTableList} />
		</span>
		<h1>Toodoo app</h1>	
	</div>
	
	<button on:click={toggleModal}>
		Add New todo
	</button>
	<Modal {isModalOpen} {toggleModal} {submitFormHandler}  {folderList}/>
</header>

<style>
	header { 
		grid-area: header; 
		display:  flex;
		justify-content: space-between;
		align-items: center;
		border-bottom:  1px solid lightgray;
		background:  white; 
	}

	header button {
		max-height: 40px;
    	padding: 10px;
    	text-align: center;
	}
	.left-header {
		display: flex;
		align-items: center;
	}
	.fa-icon {
		margin-right: 5px;
		font-size: 1.5rem;
		cursor: pointer;
	}
	.fa-icon:hover {
		transform:  scale(1.2);
	}
	button {
		border: none;
    	background: black;
    	color: white;
    	font-weight: 500;
    	border-radius: 5px;
    	cursor:  pointer;
	}
	button:hover {
		box-shadow: rgb(0 0 0 / 20%) 0px 0px 3px 1px;
	}
</style>