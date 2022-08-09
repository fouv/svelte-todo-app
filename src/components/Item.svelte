<script>

	import { createEventDispatcher } from "svelte";

	export let id, text, complete;

	const dispatch = createEventDispatcher();

function triggerUpdate() {
	dispatch("update", { id, text, complete });
}

function handleDoubleClick(){
	const yes = confirm("Vous êtes certain de vouloir supprimer cet article ?")
	if (yes) { 
			dispatch("delete", id);
	}
}
</script>

<style>
	.item {
		display:flex;
		align-items:center;
		padding:15px;
		background: #ffffff;
	}

	.item:focus-within {
		background: rgba(255, 255, 255, 0.8);
	}

	.text-input {
		flex-grow:1;
		background: none;
		border: none;
		outline:none;
		font-weight: 500;
		font-size:1em;
	}

	.completed-checkbox {
		margin-left:15px;
}
	.item.completed {
		background:#dddddd;
	}

	.item.completed .text-input {
		color: #555555;
		text-decoration: line-through;
	}
</style>
<!-- on:keyup permet de perdre le focus quand on clique sur enter-->
<!-- on:blur quand le focus est retiré de l'élément courant-->
<div class="item" class:complete on:dblclick={handleDoubleClick}>
	<input 
		class="text-input" 
		type="text" 		
		bind:value={text} 
		readonly={complete} 
		on:keyup={({ key, currentTarget }) => key === 'Enter' && currentTarget.blur()}
		on:blur={()=> triggerUpdate()}/>
	<input 
		class="complete-checkbox" 
		type="checkbox" 	
		bind:checked={complete}
		on:change={() => triggerUpdate()}/>
</div>