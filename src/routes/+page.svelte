<script>
  import { onMount, onDestroy } from "svelte";

  let currentIndex = 0;
  const images = [
    "https://images.pexels.com/photos/327434/pexels-photo-327434.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1",
    "https://images.pexels.com/photos/533854/pexels-photo-533854.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1",
    "https://images.pexels.com/photos/389724/pexels-photo-389724.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1",
    "https://images.pexels.com/photos/433524/pexels-photo-433524.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1"
  ];

  const slideInterval = 3000;

  onMount(() => {
    const interval = setInterval(() => {
      currentIndex = (currentIndex + 1) % images.length;
    }, slideInterval);

    onDestroy(() => {
      clearInterval(interval);
    });
  });
</script>

<div class="slider-container">
  <div class="slider" style="transform: translateX({-currentIndex * 100}%)">
    {#each images as image, index}
      <img src={image} alt={`slide-${index}`} class="slide" />
    {/each}
  </div>
  <div class="progress-bar">
    {#each images as _, index}
      <div class="progress-bar-child {index === currentIndex || index <= currentIndex ? 'active' : ''}">
        <!-- Child element that fills its parent width based on currentIndex -->
        <div class="progress-bar-fill"></div>
      </div>
    {/each}
  </div>
</div>

<style>
  @import "../index.css";
</style>