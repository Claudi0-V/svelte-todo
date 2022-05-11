<script lang="ts">
	export let currentViewItems;
</script>

<main>
	{#each currentViewItems as todoFolder (todoFolder.id)}
	<ul>
		{#each todoFolder.items as todo (todo.dueDate) }
		<li>
			<h2>{todo.title}</h2>
			<p>{todo.description}</p>
			<span>{todo.priority}</span>
			<span>{todo.dueDate}</span>			
		</li>
		{/each}
	</ul>
	{/each}
</main>
