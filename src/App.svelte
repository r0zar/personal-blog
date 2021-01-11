<script>
  import Tailwindcss from "./Tailwind.svelte";
  import anime from "animejs/lib/anime.es.js";
  import { onMount } from "svelte";
  import GhostContentAPI from "@tryghost/content-api";
  const api = new GhostContentAPI({
    url: "https://blog.rossragsdale.com",
    key: "b17cb2756c8fc3ec3c0e718842",
    version: "v3",
  });
  let postList = [];
  let loaded = false;
  // fetch 5 posts, including related tags and authors
  api.posts
    .browse({ limit: 5, include: "tags,authors" })
    .then((posts) => {
      postList = [posts[0]];
      loaded = true;
    })
    .catch((err) => {
      console.error(err);
    });
  let faDiscord;
  let faTwitter;
  let faGithub;
  let faLinkedIn;
  let faSoundclound;
  onMount(() => {
    faDiscord = document.querySelector(".fa-discord");
    faDiscord.addEventListener("mouseenter", enterElement, false);
    faDiscord.addEventListener("mouseleave", leaveElement, false);
    faTwitter = document.querySelector(".fa-twitter");
    faTwitter.addEventListener("mouseenter", enterElement, false);
    faTwitter.addEventListener("mouseleave", leaveElement, false);
    faGithub = document.querySelector(".fa-github");
    faGithub.addEventListener("mouseenter", enterElement, false);
    faGithub.addEventListener("mouseleave", leaveElement, false);
    faLinkedIn = document.querySelector(".fa-linkedin-in");
    faLinkedIn.addEventListener("mouseenter", enterElement, false);
    faLinkedIn.addEventListener("mouseleave", leaveElement, false);
    faSoundclound = document.querySelector(".fa-soundcloud");
    faSoundclound.addEventListener("mouseenter", enterElement, false);
    faSoundclound.addEventListener("mouseleave", leaveElement, false);
  });
  function animateElement(element, scale, duration, elasticity) {
    anime.remove(element);
    anime({
      targets: element,
      scale: scale,
      duration: duration,
      elasticity: elasticity,
    });
  }
  function enterElement(e) {
    animateElement(e.target, 2, 800, 400);
  }
  function leaveElement(e) {
    animateElement(e.target, 1, 600, 300);
  }
</script>

<Tailwindcss />

<nav>
  <div class="md:flex items-center justify-between py-3 px-8 md:px-12">
    <div class="flex justify-between items-center">
      <div class="text-2xl font-bold text-gray-800 md:text-3xl">
        <a href="/">🚀</a>
      </div>
      <div class="md:hidden">
        <button
          type="button"
          class="block text-gray-800 hover:text-gray-700 focus:text-gray-700 focus:outline-none">
          <svg class="h-6 w-6 fill-current" viewBox="0 0 24 24">
            <path
              class="hidden"
              d="M16.24 14.83a1 1 0 0 1-1.41 1.41L12 13.41l-2.83 2.83a1 1 0 0 1-1.41-1.41L10.59 12 7.76 9.17a1 1 0 0 1 1.41-1.41L12 10.59l2.83-2.83a1 1 0 0 1 1.41 1.41L13.41 12l2.83 2.83z"
            />
            <path
              d="M4 5h16a1 1 0 0 1 0 2H4a1 1 0 1 1 0-2zm0 6h16a1 1 0 0 1 0 2H4a1 1 0 0 1 0-2zm0 6h16a1 1 0 0 1 0 2H4a1 1 0 0 1 0-2z"
            />
          </svg>
        </button>
      </div>
    </div>
    <div class="flex flex-col md:flex-row hidden md:block -mx-2">
      <a
        href="/"
        class="text-gray-800 rounded hover:bg-gray-600 hover:text-gray-100 hover:font-medium py-2 px-2 md:mx-2"
        >Home</a
      >
      <a
        href="https://blog.rossragsdale.com"
        class="text-gray-800 rounded hover:bg-gray-600 hover:text-gray-100 hover:font-medium py-2 px-2 md:mx-2"
        >Blog</a
      >
      <a
        href="https://pointblankdev.com"
        class="text-gray-800 rounded hover:bg-gray-600 hover:text-gray-100 hover:font-medium py-2 px-2 md:mx-2"
        >Point Blank Dev</a
      >
    </div>
  </div>
</nav>
<main class="text-center lg:max-w-none max-w-sm mx-auto flex-grow px-1">
  <h1 class="py-3 text-5xl font-extralight text-blue-400">Hey, I'm Ross</h1>
  <div class="lg:w-1/2 mx-auto mt-6 font-light">
    <p>I'm a freelance web developer.</p>
    <p>I work on complex problems to make them simple.</p>
    <p class="mt-4">
      I founded Point Blank Dev to help others achieve their goals and building
      amazing products.
    </p>
  </div>
  <section class="py-12">
    <h1 class="py-3 text-3xl font-light">Latest blog post</h1>
    <div class="container mx-auto lg:w-1/2">
      <div class="flex flex-col">
        {#if !loaded}
          <div class="w-full md:px-4 lg:px-6 py-5">
            <div
              class="bg-white px-4 hover:shadow-md shadow rounded-lg cursor-pointer"
            >
              <i class="animate-spin fas fa-spinner p-10" />
            </div>
          </div>
        {:else}
          {#each postList as post}
            <div class="w-full md:px-4 lg:px-6 py-5">
              <div
                class="bg-white px-4 hover:shadow-md shadow rounded-lg cursor-pointer"
              >
                <a href={post.url} class="px-4 py-4 md:px-10">
                  <h3 class="font-normal text-md">{post.title}</h3>
                  <p class="py-4 font-thin">
                    {post.excerpt}
                  </p>
                  <div class="flex flex-wrap pt-2">
                    <div class="w-full text-sm font-light">
                      {new Date(post.created_at).toLocaleDateString()}
                    </div>
                  </div>
                </a>
              </div>
            </div>
          {/each}
        {/if}
      </div>
    </div>
  </section>
</main>
<footer>
  <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 1440 320">
    <path
      fill="#0099ff"
      fill-opacity="1"
      d="M0,160L48,181.3C96,203,192,245,288,229.3C384,213,480,139,576,106.7C672,75,768,85,864,106.7C960,128,1056,160,1152,192C1248,224,1344,256,1392,272L1440,288L1440,320L1392,320C1344,320,1248,320,1152,320C1056,320,960,320,864,320C768,320,672,320,576,320C480,320,384,320,288,320C192,320,96,320,48,320L0,320Z"
    />
  </svg>
  <div
    class="-mt-12 pb-6 lg:pb-12 mx-auto left-0 right-0 text-center cursor-default"
    style="background: #0099ff"
  >
    <a href="https://discord.gg/StNEj3trxt"
      ><i
        class="text-gray-200 hover:text-white text-xl p-2 mx-1 fab fa-discord"
      /></a
    >
    <a href="https://twitter.com/lordrozar"
      ><i
        class="text-gray-200 hover:text-white text-xl p-2 mx-1 fab fa-twitter"
      /></a
    >
    <a href="https://github.com/r0zar"
      ><i
        class="text-gray-200 hover:text-white text-xl p-2 mx-1 fab fa-github"
      /></a
    >
    <a href="https://www.linkedin.com/in/rossragsdale/"
      ><i
        class="text-gray-200 hover:text-white text-xl p-2 mx-1 fab fa-linkedin-in"
      /></a
    >
    <a href="https://soundcloud.com/rozarbeats"
      ><i
        class="text-gray-200 hover:text-white text-xl p-2 mx-1 fab fa-soundcloud"
      /></a
    >
  </div>
</footer>

<style>
  /* none */
</style>
