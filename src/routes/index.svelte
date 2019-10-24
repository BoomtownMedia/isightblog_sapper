<script>
  import { onMount } from "svelte";
  import Header from "../components/Header.svelte";
  import Footer from "../components/Footer.svelte";
  import Video from "../components/Video.svelte";

  let posts = [];
  let videos = [];

  let offset = 0;

  onMount(async function() {
    const response = await fetch("https://blog-api-isight.herokuapp.com/posts");
    posts = await response.json();
    
    window.addEventListener("scroll", parallaxShift);
  });

  function parallaxShift() {
    offset = window.pageYOffset;
  }

  function convertToSlug(title) {
    return title.toLowerCase()
      .replace(/[^\w ]+/g, "")
      .replace(/ +/g, "-");
  }


</script>

<style>
  .img {
    width: 100%;
    height: 200px !important;
    object-fit: cover;
  }
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

<div
  class="main main-raised"
  style="top: -{offset / 2}px; padding-top: 20px; margin-bottom: -{offset / 2}px">
  <div class="container">
    <div class="section">
      <h2 class="title text-center">Latest Blog Posts</h2>
      <br />
      <div class="row justify-content-center">

        <!--Begin Two Column Cards-->
        {#each posts.slice(0, 1) as post}
          <div class="col-md-6">
            <a rel="prefetch" href={convertToSlug(post.title)}>

              <div
                class="card card-raised card-background"
                style="background-image: url('{post.imageBackdrop.url}')">
                <div class="card-body">
                  <h3 class="card-title">{post.title}</h3>
                  <p class="card-description">
                    {post.subtitle.slice(0, 200)}...
                  </p>
                  <button class="btn btn-danger btn-round">Read Article</button>
                </div>
              </div>

            </a>
          </div>
        {/each}

        <!--End Two columns cards-->
        <!--Begin Two Column Cards-->
        {#each posts.slice(1, 2) as post}
          <div class="col-md-6">
            <a rel="prefetch" href={convertToSlug(post.title)}>

              <div
                class="card card-raised card-background"
                style="background-image: url('{post.imageBackdrop.url}')">
                <div class="card-body">
                  <h3 class="card-title">{post.title}</h3>
                  <p class="card-description">
                    {post.subtitle.slice(0, 200)}...
                  </p>
                  <button class="btn btn-warning btn-round">
                    Read Article
                  </button>
                </div>
              </div>

            </a>
          </div>
        {/each}

        <!--End Two columns cards-->

        <!--Single Column Card with Background-->
        <div class="col-md-12">
          {#each posts.slice(2, 3) as post}
            <a rel="prefetch" href={convertToSlug(post.title)}>

              <div
                class="card card-raised card-background"
                style="background-image: url('{post.imageBackdrop.url}')">
                <div class="card-body">
                  <h3 class="card-title">{post.title}</h3>
                  <p class="card-description">
                    {post.subtitle.slice(0, 200)}...
                  </p>
                  <button class="btn btn-primary btn-round">
                    Read Article
                  </button>
                </div>
              </div>

            </a>
          {/each}
        </div>

        <!--End Single Column Card with Background-->

        <div class="section">
          <h3 class="title text-center">Other posts</h3>
          <br />
          <div class="row">
            {#each posts.slice(3, posts.length + 1) as post}
              <div class="col-md-4">
                <div class="card card-blog">
                  <div class="card-header card-header-image">
                    <a href={convertToSlug(post.title)}>
                      <img
                        class="img img-raised"
                        src={post.imageBackdrop.url} />
                    </a>
                  </div>
                  <div class="card-body">
                    <h4 class="card-title">
                      <a href={convertToSlug(post.title)}>{post.title}</a>
                    </h4>
                    <p class="card-description">
                      {post.subtitle}
                      <a href={convertToSlug(post.title)}>Read More</a>
                    </p>
                    <p class="author">
                      by
                      <a href={post.slug}>
                        <b>{post.author}</b>
                        {new Date(post.createdAt).toLocaleDateString(
                          'default',
                          { weekday: 'long', month: 'long', day: 'numeric' }
                        )}
                      </a>
                    </p>
                  </div>
                </div>
              </div>
            {/each}
          </div>
        </div>
        <div class="container">
          <h2 class="title text-center">Videos</h2>
        </div>
        <!--End Sug-->

        <Video />
      </div>
    </div>
  </div>
</div>
<Footer />
