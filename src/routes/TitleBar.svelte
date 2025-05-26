<script lang="ts">
  let { pagenumber } = $props();

  const titles = [
    "Get to know our sustainability events",
    "Learn more about educational events",
    "Check out our sustainability products",
    "What's Blooming & What's Visiting",
  ];
</script>

<div class="relative w-full flex justify-between mt-10">
  <div class="absolute top-[80%] left-0 right-0 h-[2px] bg-gray-200 z-0"></div>

  {#each titles as title, index}
    <div class="relative z-10 flex flex-col items-center text-center">
      <span
        class="mb-5 text-sm
        {pagenumber === index ? 'text-black font-semibold' : 'text-gray-300'}"
      >
        {title}
      </span>
      <div
        class="w-6 h-6 flex items-center justify-center rounded-full border-2
        transition-all duration-300 bg-white
        {pagenumber === index
          ? 'border-black text-black'
          : 'border-gray-300 text-gray-300'}"
      >
        {#if pagenumber === index}
          <span class="text-xs font-bold">✔</span>
        {/if}
      </div>
    </div>
  {/each}
</div>
