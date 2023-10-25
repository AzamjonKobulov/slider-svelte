<script>
  import { onMount, onDestroy } from "svelte";

  export let images = [];
  export let slideInterval = 1000;

  let currentIndex = 0;
  let interval;

  function handleProgressBarClick(index) {
    currentIndex = index;
  }

  onMount(() => {
    interval = setInterval(() => {
      currentIndex = (currentIndex + 1) % images.length;
    }, slideInterval);

    return () => {
      clearInterval(interval);
    };
  });
</script>

<div class="slider-container">
  <div class="slider" style="transform: translateX(-{currentIndex * 100}%)">
    {#each images as image, index}
      <img src={image} alt={`slide-${index}`} class="slide" />
    {/each}
  </div>
  <div class="progress-bar">
    {#each images as _, index}
      <div
        class={`progress-bar-child ${index === currentIndex ? 'active' : index < currentIndex ? 'filled' : ''}`}
        on:click={() => handleProgressBarClick(index)}
      >
        <div class="progress-bar-fill"></div>
      </div>
    {/each}
  </div>
</div>

<style>
  @import "./styles.module.pcss";
</style>
