<svelte:head>
	<meta charset="utf-8">
	<meta name="viewport" content="width=device-width, initial-scale=1">
	<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bulma@1.0.2/css/bulma.min.css">
</svelte:head>

<script>
	let obj = $state({id: 0});

	/* localhost api for
	PHP
	function enableCORS(Response $response) {
	    return $response
		->withHeader('Content-Type', 'application/json')
		->withHeader('Access-Control-Allow-Origin', '*')
		->withHeader('Access-Control-Allow-Headers', '*')
		->withHeader('Access-Control-Allow-Methods', '*');
	}
	*/
	$effect(() => {
		if (!!obj.id && obj.id > 0) {
			new Promise(res => {
				setTimeout(res, 2000)
			})
			.then(() => fetch(`http://localhost/hi`))
      .then(response => response.json())
      .then(json => {
				debugger;
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

	const json = {
		
	}
</script>
<!-- https://bulma.io/documentation/form/general/ -->
<div class="container" style="padding: 1rem">
	<div class="columns">
	  <div class="column">
			<form method="post" enctype="multipart/form-data" onsubmit={handleSubmit}>
				<!-- <label>ID:
				<input type="number" bind:value={obj.id} min="0" max="10" />
				</label> -->
				{#each [ "a", "b", "c" ] as name}
					<div class="field is-horizontal">
					  <div class="field-label is-normal">
					    <label class="label" for="name">Name</label>
					  </div>
						 <div class="field-body">
					    <div class="field">
					      <div class="control">
					        <input class="input" id="name" type="text" placeholder="">
								</div>
					      <!-- <p class="help is-danger">
					        This field is required
					      </p> -->
					    </div>
					  </div>
					</div>
				{/each}
				<input type="submit" value="submit">
			</form>
		</div>
	</div>
</div>



<br>
{JSON.stringify(obj)}
