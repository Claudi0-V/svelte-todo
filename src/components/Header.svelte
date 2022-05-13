<script lang="ts">
	import type { TodoProject } from './classes/NewProject.svelte';
	import type { Todo } from './classes/NewTodo.svelte';
	import Modal from './Modal.svelte'

	export let globalFolder: TodoProject[];
	export let folderList: string[];
	let isModalOpen: boolean = true;
	
	const toggleModal = ():void => {isModalOpen = !isModalOpen};
	const submitFormHandler = (todo: Todo, folderName: string): void => {
		const folderIndex = globalFolder.findIndex(folder => folder.name === folderName);
		globalFolder[folderIndex].items.push(todo);
		globalFolder = globalFolder;
	}


</script>

<header>
	<h1>Toodoo app</h1>
	<button on:click={toggleModal}>
		Add New todo
	</button>
	<Modal {isModalOpen} {toggleModal} {submitFormHandler}  {folderList}/>
</header>