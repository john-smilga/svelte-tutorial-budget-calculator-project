<script>
  import { blur, fade, fly } from "svelte/transition";
</script>

<div class="modal-container" in:blur out:fade>
  <div class="modal-content" transition:fly={{ y: 200, delay: 500 }}>
    <slot />
  </div>
</div>
