<style>
main {
  text-align: center;
  padding: 1em;
  max-width: 240px;
  margin: 0 auto;
  flex-grow: 1;
}

footer > svg {
  margin-bottom: -3px;
}

h1 {
  font-size: 4em;
  font-weight: 100;
}

@media (min-width: 640px) {
  main {
    max-width: none;
  }
}
</style>

<script>
export let name;
import anime from "animejs/lib/anime.es.js";
import { onMount } from "svelte";
onMount(() => {
  const svgPath = document.querySelectorAll(".path");
  const svgText = anime({
    targets: svgPath,
    loop: false,
    direction: "alternate",
    strokeDashoffset: [anime.setDashoffset, 0],
    easing: "easeInOutSine",
    duration: 700,
    delay: (el, i) => {
      return i * 120;
    },
  });
});
</script>

<main>
  <h1>hi, i'm ross</h1>
  <p>Welcome to my site.</p>
</main>
<footer>
  <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 1440 320">
    <path
      class="path"
      fill="#0099ff"
      fill-opacity="1"
      d="M0,160L48,181.3C96,203,192,245,288,229.3C384,213,480,139,576,106.7C672,75,768,85,864,106.7C960,128,1056,160,1152,192C1248,224,1344,256,1392,272L1440,288L1440,320L1392,320C1344,320,1248,320,1152,320C1056,320,960,320,864,320C768,320,672,320,576,320C480,320,384,320,288,320C192,320,96,320,48,320L0,320Z"
      ></path>
  </svg>
</footer>
