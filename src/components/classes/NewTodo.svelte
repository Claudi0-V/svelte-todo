<script context="module" lang="ts">
	export interface Todo {
		title:string, 
		description: string, 
		priority: string,
		dueDate: string, 
	}

</script>

<script lang="ts">
	
	export class NewTodo implements Todo {
		constructor(public title:string, 
					public description: string = '', 
					public priority: string,
					public dueDate: string = new Date().toJSON(), 
					){
		}
	}
</script>