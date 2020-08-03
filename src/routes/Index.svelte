<script>
  import Repl from "@sveltejs/svelte-repl";
  let isLoading = false;
  let repl;
  let offset = 1;

  $: if (repl) {
    repl.set({ components: [{ name: "App", type: "svelte", source: "whee" }] });
  }
</script>

<style>
  .viewport {
    display: grid;
    width: 300%;
    height: 100%;
    grid-template-columns: 33.333% 66.666%;
    transition: transform 0.3s;
    grid-auto-rows: 100%;
  }

  .repl-container.loading {
    opacity: 0.6;
  }

  /* temp fix for #2499 and #2550 while waiting for a fix for https://github.com/sveltejs/svelte-repl/issues/8 */

  .repl-container :global(.tab-content),
  .repl-container :global(.tab-content.visible) {
    pointer-events: all;
    opacity: 1;
  }
  .repl-container :global(.tab-content) {
    visibility: hidden;
  }
  .repl-container :global(.tab-content.visible) {
    visibility: visible;
  }
</style>

<h2>Haim</h2>
<div class="viewport offset-{offset}">

  <div class="repl-container" class:loading={isLoading}>
    <Repl bind:this={repl} workersUrl="workers" relaxed />
  </div>
</div>
