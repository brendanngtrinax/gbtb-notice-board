<script lang="ts">
  import Card from "./Card.svelte";
  let {
    pagenumber,
    flipstatus,
  }: { pagenumber: number; flipstatus: boolean[] } = $props();
  import { cards } from "./carddata";
</script>

<div class="flex justify-center items-center mt-10">
  {#each cards as page, i}
    {#if i === pagenumber}
      <div
        class="grid grid-cols-2 place-items-center gap-6 xl:grid-cols-none xl:grid-none xl:flex xl:justify-between xl:items-start w-full"
      >
        {#each page as card, j}
          <Card data={card} isFlipped={flipstatus[j]} />
        {/each}
      </div>
    {/if}
  {/each}
</div>
