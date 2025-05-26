<script lang="ts">
  import "../app.css";

  let { children } = $props();
</script>

<img class="absolute z-[-20]" src="/background.png" alt="background" />

{@render children()}
