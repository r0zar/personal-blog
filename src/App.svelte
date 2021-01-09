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
  // fetch 5 posts, including related tags and authors
  api.posts
    .browse({ limit: 5, include: "tags,authors" })
    .then((posts) => {
      postList = posts;
    })
    .catch((err) => {
      console.error(err);
    });
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

<Tailwindcss />

<nav>
  <div class="md:flex items-center justify-between py-3 px-8 md:px-12">
    <div class="flex justify-between items-center">
      <div class="text-2xl font-bold text-gray-800 md:text-3xl">
        <a href="/">✨</a>
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
        class="text-gray-800 rounded hover:bg-gray-900 hover:text-gray-100 hover:font-medium py-2 px-2 md:mx-2"
        >Home</a
      >
      <a
        href="#"
        class="text-gray-800 rounded hover:bg-gray-900 hover:text-gray-100 hover:font-medium py-2 px-2 md:mx-2"
        >About</a
      >
      <a
        href="#"
        class="text-gray-800 rounded hover:bg-gray-900 hover:text-gray-100 hover:font-medium py-2 px-2 md:mx-2"
        >Contact</a
      >
    </div>
  </div>
</nav>
<main>
  <h1 class="pt-2">Hey, I'm Ross</h1>
  <p class="py-1">Welcome to my site 👋</p>
  <section class="py-12">
    <div class="container mx-auto lg:w-1/2">
      <div class="flex flex-col">
        {#each postList as post}
          <div class="w-full md:px-4 lg:px-6 py-5">
            <div
              class="bg-white px-4 hover:shadow-md shadow rounded-lg cursor-pointer"
            >
              <!-- <div class="rounded-lg rounded-b-none">
                <img
                  src="{post.feature_image}"
                  alt="{post.title}"
                  class="w-full h-48 object-cover rounded-lg rounded-b-none " />
              </div> -->
              <a href={post.url} class="px-4 py-4 md:px-10">
                <h3 class="font-bold text-md">{post.title}</h3>
                <p class="py-4">
                  {post.excerpt}
                </p>
                <div class="flex flex-wrap pt-8">
                  <div class="w-full text-sm font-medium">
                    {new Date(post.created_at).toLocaleDateString()}
                  </div>
                </div>
              </a>
            </div>
          </div>
        {/each}
      </div>
    </div>
  </section>
</main>
<footer>
  <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 1440 320">
    <path
      class="path"
      fill="#0099ff"
      fill-opacity="1"
      d="M0,160L48,181.3C96,203,192,245,288,229.3C384,213,480,139,576,106.7C672,75,768,85,864,106.7C960,128,1056,160,1152,192C1248,224,1344,256,1392,272L1440,288L1440,320L1392,320C1344,320,1248,320,1152,320C1056,320,960,320,864,320C768,320,672,320,576,320C480,320,384,320,288,320C192,320,96,320,48,320L0,320Z"
    />
  </svg>
</footer>

<style>
  main {
    text-align: center;
    max-width: 320px;
    margin: 0 auto;
    flex-grow: 1;
  }

  footer > svg {
    bottom: 0;
    z-index: -1;
  }

  h1 {
    font-size: 4em;
    font-weight: 100;
    color: #0099ff;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
</style>
