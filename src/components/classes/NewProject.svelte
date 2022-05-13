<script context="module" lang="ts">
	import type { Todo } from "./NewTodo.svelte";
	import { idGenerator } from '../utils';
	
	export interface TodoProject {
		name: string,
		items: Todo[];
		id: string;
	}


	export class Project {
		constructor(
			public name: string,
			public items: Todo[] = [],
			public id: string = idGenerator(),
		) {}
	}
</script>
