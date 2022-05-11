<script lang="ts">
	import Sidebar from "./components/Sidebar.svelte";
	import Header from "./components/Header.svelte";
	import Main from "./components/Main.svelte";
	import type { TodoProject } from "./components/classes/NewProject.svelte";

	let globalFolder: TodoProject[] = [
		{
			name: "Daily",
			id: "2022-05-10T14:12:09.944Z",
			items: [
				{
					title: "wake up",
					description: "get up of the bed",
					dueDate: "2022-05-10T14:20:05.331Z",
					priority: "low",
				},
				{
					title: "drink coffee",
					description: "make coffee and drink",
					dueDate: "2022-05-10T14:20:41.428Z",
					priority: "low",
				},
			],
		},
		{
			name: "Work",
			id: "2022-05-10T14:12:32.848Z",
			items: [
				{
					title: "talk back to boss",
					description: "i'm fed up with this guy",
					dueDate: "2022-05-10T14:23:14.454Z",
					priority: "high",
				},
				{
					title: "shit on his desk",
					description: "I'm done!",
					dueDate: "2022-05-10T14:23:42.746Z",
					priority: "high",
				},
			],
		},
		{
			name: "Other",
			id: "2022-05-10T14:12:45.791Z",
			items: [
				{
					title: "dunno",
					description: "i really don't",
					dueDate: "2022-05-10T14:30:31.628Z",
					priority: "low",
				},
				{
					title: "watch movie",
					description: "nothing else",
					dueDate: "2022-05-10T14:30:47.964Z",
					priority: "low",
				},
			],
		},
	];

	let currentViewItems: TodoProject[] = [...globalFolder];
	let isModalOpen: boolean = false;

	function folderChangeHandler(name: string): void {
		const arr = globalFolder.filter((folder) => {
			if (name === 'all') return true;
			return folder.name === name;
		});
		currentViewItems = arr;
	}
</script>

<div id="root">
	<Header />
	<Sidebar {globalFolder} onFolderChange="{folderChangeHandler}" />
	<Main {currentViewItems} />
</div>

<style></style>
