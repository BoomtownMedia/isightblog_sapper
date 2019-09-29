<script>
  import { onMount } from "svelte";

  export let pageData = {};
  let posts = [];
  let slug;

  onMount(async function() {
    const response = await fetch("https://blog-api-isight.herokuapp.com/posts");
    posts = await response.json();
    posts = posts.filter(i => window.location.pathname.includes(i.slug));
    pageData = posts[0];
  });
</script>

<svelte:head>
  <title>{pageData.title}</title>
</svelte:head>

<div class="content">
  <h1>{pageData.title}</h1>
  <h2>{pageData.subtitle}</h2>
  <p>{pageData.postBody}</p>
</div>
