<script lang="ts">
  import CircularProgress from "$lib/CircularProgress.svelte";

  export let pagenumber: number = 0;
  export let totalPages: number = 4;
</script>

<div class="flex justify-center items-center gap-2 text-xl mt-20">
  <!-- Rotating loader -->
  <CircularProgress />
  <!-- Dot indicators -->
  <div class="flex gap-4">
    {#each Array(totalPages) as _, i}
      <div
        class={`w-4 h-4 rounded-full ${i === pagenumber ? "bg-black" : "bg-gray-300"}`}
      ></div>
    {/each}
  </div>

  <!-- Text description -->
  <span class="ml-6">
    {pagenumber + 1} of {totalPages}
    Sustainability events in preview
  </span>
</div>
