<script>
	export let toggle;
</script>

<span class="close-button" on:click={toggle}>+</span>

<style>

.close-button {
 	font-size: 25px;
 	position: absolute;
  	top: -2px;
 	right: 7px;
  	transform: rotate(45deg);
  	cursor: pointer;
}

</style>