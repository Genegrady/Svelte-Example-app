<script>

	import { onMount } from "svelte"
	const URL = `https://www.swapi.co/api/planets/`
	
	let posts = [];

  (async () => {
    const res = await fetch(URL);
    posts = (await res.json()).results;
    console.log(posts)
  })();

	// for the await block
	let planets = fetch(URL)
		.then((res) => res.json())

</script>

<div>
	<h1>
    	<img src="https://api.time.com/wp-content/uploads/2015/07/earth-blue-marble-dscvr.jpg" />
		<p class="about">
				Planets
		</p>
	</h1>
{#await planets}
<div>
	Searching for Planets....
</div>
{:then response}
{#each response.results as planet}
	<div class="container">
            <div class="card">
                <div class="card-body">
                    <h3>Name: {planet.name}</h3>
                    <p> Population: {planet.population} </p>
                </div>
            </div>
	</div>
	{:else}
	<p class="card"> No Planets</p>
{/each}
{/await}
</div>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>