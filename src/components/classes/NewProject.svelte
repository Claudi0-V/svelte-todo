<script context="module" lang="ts">
	import type { Todo } from "./NewTodo.svelte";

	export interface TodoProject {
		name: string;
		items: Todo[];
		id: string;
	}


	export class Project {
		constructor(
			public name: string,
			public items: Todo[] = [],
			public id: string = new Date().toJSON()
		) {}
	}
</script>
