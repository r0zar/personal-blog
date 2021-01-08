<script>
	import successkid from 'images/successkid.jpg';
	import anime from "animejs";
  	import { onMount } from 'svelte'
  	onMount(()=> {
		// anime({
		// 	targets: 'img',
		// 	translateX: 250,
		// 	rotate: '1turn',
		// 	backgroundColor: '#FFF',
		// 	duration: 800
		// });
	})
</script>
  
<style>
	h1, figure, p {
		text-align: center;
		margin: 0 auto;
	}

	h1 {
		font-size: 2.8em;
		text-transform: uppercase;
		font-weight: 700;
		margin: 0 0 0.5em 0;
	}

	figure {
		margin: 0 0 1em 0;
	}

	img {
		width: 100%;
		max-width: 400px;
		margin: 0 0 1em 0;
	}

	p {
		margin: 1em auto;
	}

	@media (min-width: 480px) {
		h1 {
			font-size: 4em;
		}
	}
</style>

<svelte:head>
	<title>Sapper project template</title>
</svelte:head>

<h1>🚧 Work in progress 🚧</h1>

<figure>
	<figcaption>I'll have something up and running soon. 👷‍♂️</figcaption>
</figure>
