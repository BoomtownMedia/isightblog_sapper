<script>
  import { onMount } from "svelte";
  let posts = [];

  onMount(async function() {
    const response = await fetch("https://blog-api-isight.herokuapp.com/posts");
    posts = await response.json();
  });
</script>

<svelte:head>
  <title>Blog</title>
</svelte:head>

<ul>
  {#each posts as post}
    <li>
      <a rel="prefetch" href="blog/{post.slug}">{post.title}</a>
    </li>
  {/each}
</ul>
