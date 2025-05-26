<script lang="ts">
  import "../app.css";

  let { children } = $props();
</script>

<img class="absolute" src="/background.png" alt="background" />

{@render children()}
