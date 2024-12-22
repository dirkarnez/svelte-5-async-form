<script>
	let obj = $state({id: 0});

	$effect(() => {
		if (!!obj.id && obj.id > 0) {
			new Promise(res => {
				setTimeout(res, 2000)
			})
			.then(() => fetch(`https://jsonplaceholder.typicode.com/todos/${obj.id}`))
      .then(response => response.json())
      .then(json => {
				obj = {...json, id: obj.id};
			})
		}
	});
</script>

<label>ID:
<input type="number"  bind:value={obj.id} min="0" max="10" />
</label>
<br>
{JSON.stringify(obj)}

