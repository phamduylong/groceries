<script>
  import Trash from "lucide-svelte/icons/Trash";
  import { Modal } from '@skeletonlabs/skeleton-svelte';
  /**
   * @type {{ item: string, quantity: number, price: number }[]}
  */
  let items = $state(localStorage.getItem("items") ? JSON.parse(localStorage.getItem("items")) : [
  ]);

  let modalOpen = $state(false);

  $effect(() => {
    localStorage.setItem("items", JSON.stringify(items));
  });

function modalClose(deleteItem) {
  if (deleteItem) {
    // Need to know which item triggered this modal
  }
  modalOpen = false;
}
</script>

<Modal
  bind:open={modalOpen}
  triggerBase="btn preset-tonal"
  contentBase="card bg-surface-100-900 p-4 space-y-4 shadow-xl max-w-screen-sm"
  backdropClasses="backdrop-blur-sm"
>
  {#snippet content()}
    <header class="flex justify-between">
      <h2 class="h2">Delete Item</h2>
    </header>
    <article>
      <p class="opacity-60">
        Are you sure you want to delete this item? This action cannot be undone.
      </p>
    </article>
    <footer class="flex justify-end gap-4">
      <button type="button" class="btn preset-tonal" onclick={() => modalClose(false)}>Cancel</button>
      <button type="button" class="btn preset-filled" onclick={() => modalClose(true)}>Confirm</button>
    </footer>
  {/snippet}
</Modal>

<main>
  <div class="container h-full mx-auto flex justify-center items-center p-10">
    <div class="w-full space-y-10 flex flex-col items-center justify-center">
      <h1 class="h1">Items</h1>
      <div class="flex flex-col space-y-2 preset-tonal-tertiary p-10 overflow-y-scroll h-80 md:h-[450px] lg:h-[600px] container rounded-xl">
        {#each items as { item, quantity, price }, i}
          <div class="flex justify-between items-center rounded card p-4 preset-tonal-primary space-x-2 h-fit">
            <div>
              <div>{item} &times; {quantity}</div>
              <span>Total: ${(quantity * price).toFixed(2)}</span>
            </div>
            <button class="btn btn-icon preset-outlined-primary-800-200 hover:preset-filled-primary-800-200" onclick="{() => {
              items.splice(i, 1);
            }}"><Trash /></button>
          </div>
        {/each}
      </div>
    </div>
  </div>
</main>
