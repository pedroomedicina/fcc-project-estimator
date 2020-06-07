<script>
	import Table from './Table.svelte';
	import Form from './Form.svelte';

	let id;
	let name;
	let price = 5;
	/*
	extract detail and type
	*/
	function edit(e) {
		({ id, name, price } = e.detail);
	}
</script>

<style>
	main {
		flex: 1;
		align-content: center;
		justify-content: center;
		width: 80%;
		margin: 0 auto;
	}
</style>

<main>
	<h1>Project Estimator</h1>
	<Form bind:price bind:id bind:name ></Form>
	<Table on:edit={edit} ></Table>
</main>