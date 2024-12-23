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

	const handleSubmit = async e => {
		e.preventDefault();
		const formData = new FormData(e.target);
		const response = await fetch(`https://jsonplaceholder.typicode.com/posts`, {
	    method: "POST",
	    body: formData,
	  });
		const data = await response.json();
		alert(JSON.stringify(data));
	}
</script>

<form method="post" enctype="multipart/form-data" onsubmit={handleSubmit}>
	<label>ID:
	<input type="number" bind:value={obj.id} min="0" max="10" />
	</label>
	<input type="submit" value="submit">
</form>
<br>
{JSON.stringify(obj)}
