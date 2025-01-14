<script>
  import Trash from "lucide-svelte/icons/Trash";
  /**
   * @type {{ item: string, quantity: number, price: number }[]}
  */
  let items = $state(localStorage.getItem("items") ? JSON.parse(localStorage.getItem("items")) : [
  ]);

  $effect(() => {
    localStorage.setItem("items", JSON.stringify(items));
  });
</script>

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
