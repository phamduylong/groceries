<script>
  import { Trash } from "lucide-svelte";
  let items = $state([
    { item: "Item 1", price: 100 },
    { item: "Item 2", price: 200 },
    { item: "Item 3", price: 300 },
    { item: "Item 4", price: 400 },
    { item: "Item 5", price: 500 },
    { item: "Item 6", price: 600 },
    { item: "Item 7", price: 700 },
    { item: "Item 8", price: 800 },
    { item: "Item 9", price: 900 },
    { item: "Item 10", price: 1000 },
  ]);
</script>

<main>
  <div class="container h-full mx-auto flex justify-center items-center p-10">
    <div class="w-full space-y-10 flex flex-col items-center justify-center">
      <h1 class="h1">Items</h1>
      <div class="flex flex-col space-y-2 preset-tonal-tertiary p-10 overflow-y-scroll h-80 md:h-[450px] lg:h-[600px] container rounded-xl">
        {#each items as { item, price }, i}
          <div class="flex justify-between items-center rounded card p-4 preset-tonal-primary space-x-2 h-fit">
            <div>{item} - ${price}</div>
            <button class="btn btn-icon preset-outlined-primary-800-200 hover:preset-filled-primary-800-200" onclick="{() => {
              items.splice(i, 1);
            }}"><Trash /></button>
          </div>
        {/each}
      </div>
    </div>
  </div>
</main>
