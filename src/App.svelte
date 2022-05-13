<script lang="ts">
	import Sidebar from "./components/Sidebar.svelte";
	import Header from "./components/Header.svelte";
	import Main from "./components/Main.svelte";
	import { Project, TodoProject } from "./components/classes/NewProject.svelte";


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
					id: 'ida47f75b4c4a79',
				},
				{
					title: "drink coffee",
					description: "make coffee and drink",
					dueDate: "2022-05-10T14:20:41.428Z",
					priority: "low",
					id: 'id2b28e4a745d61'
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
					id: 'ida8489e4e3e91f'
				},
				{
					title: "shit on his desk",
					description: "I'm done!",
					dueDate: "2022-05-10T14:23:42.746Z",
					priority: "high",
					id: 'id4af4d79329d9c'
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
					id: 'idebf2e2129db5'
				},
				{
					title: "watch movie",
					description: "nothing else",
					dueDate: "2022-05-10T14:30:47.964Z",
					priority: "low",
					id: 'id22e0c107cd487'
				},
			],
		},
	];
	$: folderList = globalFolder.map(folder => folder.name);
	let currentFolderName: string = 'all';


	const newFolder = (folderName: string): void =>  {
		const newFolder = new Project(folderName);
		globalFolder = [...globalFolder, newFolder];
	}

	const changeFolder = (folderName: string) => currentFolderName = folderName;

</script>

<div id="root">
	<Header bind:globalFolder {folderList} />
	<Sidebar {folderList} {newFolder} {currentFolderName} {changeFolder}/>
	<Main bind:globalFolder  {currentFolderName} />
</div>

<style></style>
