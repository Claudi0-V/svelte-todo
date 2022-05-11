<script lang="ts">
	import Modal from './Modal.svelte'
	let isModalOpen: boolean = false;
	
	
	const toggleModal = () => isModalOpen = !isModalOpen;

</script>

<header>
	<h1>Toodoo app</h1>
	<button on:click={toggleModal}>
		Add New todo
	</button>
	{#if isModalOpen}
		<Modal {isModalOpen}>
			<h1>test</h1>
		</Modal>
	{/if}
</header>