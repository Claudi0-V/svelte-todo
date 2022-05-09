<script lang="ts">
	import { Todo } from './NewTodo.svelte'
	
	export class NewProject {
		constructor(public name: string, public items: Todo[] = []) {	
		}
	}

</script>