<script lang="ts">
  import type { CardType } from "$lib/types";
  import { onMount } from "svelte";
  import QRCode from "qrcode";

  let { data, isFlipped }: { data: CardType; isFlipped: boolean } = $props();
  let qrCodeDataUrl: string = $state("");

  onMount(async () => {
    try {
      qrCodeDataUrl = await QRCode.toDataURL(data.name); // Or encode another unique value like data.url
    } catch (err) {
      console.error("Failed to generate QR Code", err);
    }
  });
</script>

<div class="relative w-100 h-120 rounded-3xl preserve-3d">
  <div
    class="absolute w-full h-full bg-white p-4 flex flex-col gap-4 rounded-3xl shadow-xl backface-hidden transition-transform duration-1000"
    style="transition-timing-function: cubic-bezier(1, 0, 0, 1);"
    class:rotate-y-180={isFlipped}
  >
    <div
      class="rounded-xl bg-gray-100 h-50 bg-center bg-cover flex items-center justify-center"
      style="background-image: url({data.backgroundUrl});"
    >
      {#if !data.backgroundUrl}
        <div class="bg-gray-300 rounded-full p-4">
          <img src="/placeholder.png" alt="placeholder" class="w-6 h-6" />
        </div>
      {/if}
    </div>

    <div class="space-y-2 px-2 text-sm">
      <div class="flex items-start gap-2">
        <img src="/placeholder.png" alt="placeholder" class="w-5 h-5" />
        <div>{data.name}</div>
      </div>

      <div class="flex items-start gap-2">
        <img src="/placeholder.png" alt="placeholder" class="w-5 h-5" />
        <div>{data.description}</div>
      </div>

      <div class="flex gap-4">
        <div class="flex items-start gap-2">
          <img src="/placeholder.png" alt="placeholder" class="w-5 h-5" />
          <div>{data.date}</div>
        </div>

        <div class="flex items-start gap-2">
          <img src="/placeholder.png" alt="placeholder" class="w-5 h-5" />
          <div>{data.time}</div>
        </div>
      </div>

      <div class="flex items-start gap-2">
        <img src="/placeholder.png" alt="placeholder" class="w-5 h-5" />
        <div>{data.location}</div>
      </div>
    </div>

    <div class="flex justify-end mt-auto">
      {#if qrCodeDataUrl}
        <img src={qrCodeDataUrl} alt="QR Code" class="w-20 h-20" />
      {/if}
    </div>
  </div>

  <div
    class="absolute w-full h-full bg-white p-4 flex flex-col gap-4 rounded-3xl shadow-xl backface-hidden rotate-y-180 transition-transform duration-1000"
    style="transition-timing-function: cubic-bezier(1, 0, 0, 1);"
    class:rotate-y-0={isFlipped}
  >
    <img class="rounded-3xl" src="cardback.png" alt="back of card" />
  </div>
</div>

<style>
  /* Custom Tailwind-like classes for 3D transforms */
  .preserve-3d {
    transform-style: preserve-3d;
  }

  .backface-hidden {
    backface-visibility: hidden;
  }

  .rotate-y-180 {
    transform: rotateY(180deg);
  }

  .rotate-y-0 {
    transform: rotateY(0deg);
  }
</style>
