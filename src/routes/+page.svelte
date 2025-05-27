<script lang="ts">
  import CardDeck from "./CardDeck.svelte";
  import PageLoading from "./PageLoading.svelte";
  import TitleBar from "./TitleBar.svelte";

  let interval = 30000;

  let pagenumber = $state(0);
  let flipstatus = $state([false, false, false, false]);

  setInterval(() => {
    // 1. Start flipping before page changes
    for (let i = 0; i < flipstatus.length; i++) {
      setTimeout(() => {
        // Flip card i
        flipstatus[i] = true;

        // Flip back after 2s
        setTimeout(() => {
          flipstatus[i] = false;
        }, 2000);
      }, i * 250); // Staggered start
    }

    // 2. Change page AFTER flips start
    setTimeout(() => {
      pagenumber = (pagenumber + 1) % 4;
    }, 1000); // 1 second before interval ends
  }, interval);
</script>

<main class="p-20">
  <div class="flex items-center gap-4">
    <svg
      xmlns="http://www.w3.org/2000/svg"
      class="h-8 w-8"
      viewBox="0 0 512 512"
      ><path
        fill="currentColor"
        d="M32 456a24 24 0 0 0 24 24h400a24 24 0 0 0 24-24V176H32Zm320-244a4 4 0 0 1 4-4h40a4 4 0 0 1 4 4v40a4 4 0 0 1-4 4h-40a4 4 0 0 1-4-4Zm0 80a4 4 0 0 1 4-4h40a4 4 0 0 1 4 4v40a4 4 0 0 1-4 4h-40a4 4 0 0 1-4-4Zm-80-80a4 4 0 0 1 4-4h40a4 4 0 0 1 4 4v40a4 4 0 0 1-4 4h-40a4 4 0 0 1-4-4Zm0 80a4 4 0 0 1 4-4h40a4 4 0 0 1 4 4v40a4 4 0 0 1-4 4h-40a4 4 0 0 1-4-4Zm0 80a4 4 0 0 1 4-4h40a4 4 0 0 1 4 4v40a4 4 0 0 1-4 4h-40a4 4 0 0 1-4-4Zm-80-80a4 4 0 0 1 4-4h40a4 4 0 0 1 4 4v40a4 4 0 0 1-4 4h-40a4 4 0 0 1-4-4Zm0 80a4 4 0 0 1 4-4h40a4 4 0 0 1 4 4v40a4 4 0 0 1-4 4h-40a4 4 0 0 1-4-4Zm-80-80a4 4 0 0 1 4-4h40a4 4 0 0 1 4 4v40a4 4 0 0 1-4 4h-40a4 4 0 0 1-4-4Zm0 80a4 4 0 0 1 4-4h40a4 4 0 0 1 4 4v40a4 4 0 0 1-4 4h-40a4 4 0 0 1-4-4ZM456 64h-55.92V32h-48v32H159.92V32h-48v32H56a23.8 23.8 0 0 0-24 23.77V144h448V87.77A23.8 23.8 0 0 0 456 64"
      /></svg
    >
    <p>
      {new Date().toLocaleDateString("en-GB", {
        weekday: "long",
        day: "numeric",
        month: "long",
      })}
    </p>
  </div>
  <h1 class="text-4xl font-bold mt-4">
    Stay informed, remember the <br />
    dates and never miss out.
  </h1>
  <TitleBar {pagenumber} />
  <CardDeck {pagenumber} {flipstatus} />
  <PageLoading {pagenumber} />
</main>
