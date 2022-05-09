<script context="module" lang="ts">
	export interface Todo {
		title:string, 
		description: string, 
		dueDate: string, 
		priority: string
	}

</script>

<script lang="ts">
	

	export class NewTodo implements Todo {
		constructor(public title:string, 
					public description: string = '', 
					public dueDate: string, 
					public priority: string){
		}
	}
</script>