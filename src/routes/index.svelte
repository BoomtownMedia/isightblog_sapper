<script>
  import { onMount } from "svelte";
  import Header from "../components/Header.svelte";
  import Footer from "../components/Footer.svelte";
  let posts = [];

  let offset = 0;

  onMount(async function() {
    const response = await fetch("https://blog-api-isight.herokuapp.com/posts");
    posts = await response.json();
    window.addEventListener("scroll", parallaxShift);
  });

  function parallaxShift() {
    offset = window.pageYOffset;
  }
</script>

<style>

</style>

<svelte:head>
  <title>Isight RPV Blog</title>
</svelte:head>

<div
  class="page-header header-filter presentation-page"
  style="background-image: url('main.jpg')">
  <div class="container">
    <div class="row">
      <div class="col-md-8 ml-auto mr-auto">
        <div class="brand">
          <h1>
            ISIGHT
            <span class="pro-badge">RPV</span>
          </h1>
          <h3 class="title">
            Blog focused on unmanned aerial vehicle service industry
          </h3>
        </div>
      </div>
    </div>
  </div>
</div>

<div class="main main-raised" style="bottom: {offset / 2}px; padding-top: 20px">
  <div class="col-md-12">
    <h2 class="title text-center">Latest Blog Posts</h2>
    <br />
    <div class="row justify-content-center">

      {#each posts as post}
        <a rel="prefetch" href="blog/{post.slug}">

          <div class="col-md-4">
            <div
              class="card card-raised card-background"
              style="background-image: url('{post.imageBackdrop.url}')">
              <div class="card-body">
                <h6 class="card-category text-info">{post.category}</h6>
                <h4 class="card-title">{post.title}</h4>
                <p class="card-description">{post.subtitle.slice(0, 200)}...</p>
                <button class="btn btn-primary btn-round">Read Article</button>
              </div>
            </div>
          </div>

        </a>
      {/each}
    </div>
  </div>
</div>
<Footer />
