<script>
	import { onMount } from "svelte";
    export let id;
    // let url = "https://5f50ca542b5a260016e8bfb0.mockapi.io/api/v1/movies/"+id
    let movies = [];
    onMount(async()=>{
        const response = await fetch("https://5f50ca542b5a260016e8bfb0.mockapi.io/api/v1/movies/"+id)
        const film = await response.json();
        movies = film
        console.log(film);
    });

</script>
<main>
    <div>
        <img src={movies.image} alt="">
        <li>{movies.title}</li>
        <p>{movies.like}</p>
    </div>
</main>