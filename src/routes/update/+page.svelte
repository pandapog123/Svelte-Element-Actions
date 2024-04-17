<script lang="ts">
  import type { Action } from "svelte/action";

  const log: Action<Element, string> = (node, val) => {
    console.log("Initial value: ", val);
    return {
      update(newVal) {
        console.log(newVal);
      },
    };
  };

  let input = "";
</script>

<h1>Updates</h1>

<input type="text" bind:value={input} />

<!-- You do not need to include {input} for update to be called -->
<!-- As you could see: -->
<!-- <div use:log={input}></div> -->
<div use:log={input}>{input}</div>
