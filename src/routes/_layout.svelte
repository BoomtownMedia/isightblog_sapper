<script>
  import Nav from "../components/Nav.svelte";
  export let segment;
</script>

<style>
  main {
    max-height: 1080px;
  }
</style>

<Nav {segment} />
<main>
  <slot />
</main>
