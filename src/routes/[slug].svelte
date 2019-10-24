<script>
  import Footer from "../components/Footer.svelte";
  import { onMount } from "svelte";

  export let pageData = {};
  let posts = [];
  let slug;
  let imageURL = "";
  let encodedURL;
  let URL;
  onMount(async function() {
    const response = await fetch("https://blog-api-isight.herokuapp.com/posts");
    posts = await response.json();
    posts = posts.filter(i =>
      window.location.pathname.includes(convertToSlug(i.title))
    );
    pageData = posts[0];
    imageURL = pageData.imageBackdrop.url;

    window.addEventListener("scroll", parallaxShift);
  });

  function convertToSlug(title) {
    return title
      .toLowerCase()
      .replace(/[^\w ]+/g, "")
      .replace(/ +/g, "-");
  }

  let offset = 0;

  function parallaxShift() {
    offset = window.pageYOffset;
  }
</script>

<svelte:head>
  <title>{pageData.title}</title>
</svelte:head>

<div id="fb-root" />
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
      </div>
    </div>
  </div>
</div>
<div
  class="main main-raised"
  id="blog"
  style="bottom: {offset / 2}px; margin-bottom: -{offset / 2}px">
  <div class="container">
    <div class="section section-text">
      <div class="row">
        <div class="col-md-8 ml-auto mr-auto">
          <h3 class="title">{pageData.subtitle}</h3>
          <p>
            {@html pageData.postBody}
          </p>
        </div>
      </div>
    </div>
  </div>
  <div
    class="fb-share-button"
    data-href={window.location.href}
    data-layout="button" />
</div>
<Footer />
