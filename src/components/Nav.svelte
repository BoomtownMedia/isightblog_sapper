<script>
  export let segment;
</script>

<style>
  .selected {
    color: red;
  }
</style>

<nav>
  <ul>
    <li>
      <a
        rel="prefetch"
        class={segment === 'blog' ? 'selected' : ''}
        href="blog">
        blog
      </a>
    </li>
  </ul>
</nav>
