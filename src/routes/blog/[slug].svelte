<script>
  import { onMount } from "svelte";

  export let pageData = {};
  let posts = [];
  let slug;
  let imageURL = "";

  onMount(async function() {
    const response = await fetch("https://blog-api-isight.herokuapp.com/posts");
    posts = await response.json();
    posts = posts.filter(i => window.location.pathname.includes(i.slug));
    pageData = posts[0];
    imageURL = pageData.imageBackdrop.url;
  });
</script>

<svelte:head>
  <title>{pageData.title}</title>
</svelte:head>

<div
  class="page-header header-filter"
  data-parallax="true"
  style="background-image: url('{imageURL}')">
  <div class="container">
    <div class="row">
      <div class="col-md-8 ml-auto mr-auto text-center">
        <h1 class="title">{pageData.title}</h1>
        <h4>{pageData.subtitle}</h4>
        <br />
        <a href="#blog" class="btn btn-rose btn-round btn-lg">
          <i class="material-icons">format_align_left</i>
          Read Article
        </a>
      </div>
    </div>
  </div>
</div>
<div class="main main-raised" id="blog">
  <div class="container">
    <div class="section section-text">
      <div class="row">
        <div class="col-md-8 ml-auto mr-auto">
          <h3 class="title">{pageData.subtitle}</h3>
          <p>{pageData.postBody}</p>
        </div>
      </div>
    </div>
  </div>
</div>
