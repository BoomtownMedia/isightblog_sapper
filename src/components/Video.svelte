<script>
  import { onMount } from "svelte";
  let videos = [];

  onMount(async function() {
    const response = await fetch(
      "https://blog-api-isight.herokuapp.com/videos"
    );
    videos = await response.json();
  });
</script>

{#each videos as video}
  <div class="col-md-6">
    <div class="card">
      <div class="card-image">
        <div class="embed-responsive embed-responsive-16by9">
          <video
            width="500"
            height="315"
            src={video.media_file.url}
            poster={video.poster_img.url}
            frameborder="0"
            controls
            muted
            preload
            allowfullscreen
            style="border-radius: 20px; padding: 10px" />
        </div>
        <div class="card-body">
          <h4 class="card-title">
            <a href="#pablo">{video.title}</a>
          </h4>
        </div>

      </div>
      <!-- card image -->

    </div>
  </div>
{/each}
