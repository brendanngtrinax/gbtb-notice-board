<script lang="ts">
  import Card from "./Card.svelte";
  let { pagenumber } = $props();
  import { cards } from "./carddata";
</script>

<div class="flex justify-center items-center mt-10">
  {#each cards as page, i}
    {#if i === pagenumber}
      <div class="flex justify-between w-full">
        {#each page as card, j}
          <!-- <Card backgroundUrl={card.backgroundUrl} name={card.name} description={card.description} date={card.date} time={card.time} location={card.location} QRCode={card.QRCode}/> -->
          <Card data={card} />
        {/each}
      </div>
    {/if}
  {/each}
</div>
