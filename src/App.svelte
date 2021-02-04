<script>
	import { Router, Route, Link } from "svelte-routing";
	import Info from "./page/info.svelte";
	import Home from "./page/main.svelte";

</script>

<main>
	<Router>
		<Route path="/"><Home /></Route>
		<Route path="more/:id" component="{Info}"></Route>
	</Router>
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