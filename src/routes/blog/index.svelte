<script>
  import { onMount } from "svelte";
  import Header from "../../components/Header.svelte";
  let posts = [];

  onMount(async function() {
    const response = await fetch("https://blog-api-isight.herokuapp.com/posts");
    posts = await response.json();
  });
</script>

<style>

</style>

<svelte:head>
  <title>Isight RPV Blog</title>
</svelte:head>
<Header />

<div class="main main-raised">
  <div class="container">
    <div class="col-md-12">
      <h2 class="">Latest Blog Posts</h2>
      <br />
      <div class="row">

        {#each posts as post}
          <a rel="prefetch" href="blog/{post.slug}">

            <div class="col-md-6">
              <div
                class="card card-raised card-background"
                style="background-image: url('{post.imageBackdrop.url}')">
                <div class="card-body">
                  <h6 class="card-category text-info">{post.category}</h6>
                  <h4 class="card-title">{post.title}</h4>
                  <p class="card-description">
                    {post.subtitle.slice(0, 200)}...
                  </p>
                  <button class="btn btn-primary btn-round">
                    Read Article
                  </button>
                </div>
              </div>
            </div>

          </a>
        {/each}
      </div>
    </div>
  </div>
</div>
