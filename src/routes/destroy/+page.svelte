<script lang="ts">
  import type { Action } from "svelte/action";

  const logOnDestroy: Action<Element, number> = (_, value) => {
    return {
      destroy() {
        console.log(`Element with value ${value} is destroyed`);
      },
    };
  };

  let items = [0];
</script>

<h1>Destroy</h1>

<button on:click={() => (items = [...items, items.length])}>Add item</button>
<button
  on:click={() => {
    items = items.slice(0, items.length - 1);
  }}
>
  Remove item
</button>

{#each items as item}
  <div use:logOnDestroy={item}>Item #{item}</div>
{/each}
