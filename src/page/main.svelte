<script>
	import { Router, Route, Link } from "svelte-routing";
    import { onMount } from "svelte";
    import AutoComplete from "simple-svelte-autocomplete";
    import Image from 'svelte-image';

    let movies = [];
	onMount(async() => {
        const response = await fetch("https://5f50ca542b5a260016e8bfb0.mockapi.io/api/v1/movies");
		const film = await response.json();
		movies = film;
        console.log(movies);
    });
    // const list = movies.title;
    // var list = [];
    // movies.forEach(movie => {
    //     list.push(movie.title);
    // });
    const list = ["Handcrafted Metal Table", "Fantastic Soft Ball", "Small Metal Chicken", "Incredible Cotton Pizza", "Refined Rubber Salad",
                    "Practical Rubber Shoes", "Fantastic Concrete Chips", "Ergonomic Rubber Sausages", "Sleek Concrete Bike", , "Tasty Soft Keyboard"];
    console.log(list);
    let selector;
    $: allmovies = selector
    ? movies.filter(val => val.title.includes(selector))
    : movies;
    console.log(movies);
    let date = "";
    $: allmovies = date 
    ? movies.filter(val => new Date(val.showTime).toISOString().slice(0,10) === date)
    : movies;
    
</script>

<main>
    <!-- <input type="text" id="search" bind:value={search} class="bg-gray-200 md:focus:bg-white" placeholder="Search Movie Title" /> -->
    <AutoComplete items={list} bind:value={selector} />
    <input type="date" id="tanggal" bind:value={date} class="bg-gray-200 md:focus:bg-white" />
    {#each allmovies as movie}
        <form>
            <div>
                <Image src={movie.image} alt="" width= "50%" />
                <li>{movie.title}</li>
                <p>👍 {movie.like}</p>
                <Link to="more/{movie.id}">More Info</Link>
            </div>
        </form>
    {/each}
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}
	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>