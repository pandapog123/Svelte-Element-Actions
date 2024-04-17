<script lang="ts">
  import type { Action } from "svelte/action";

  // They only run on the client side
  // You can change the attributes of the element
  const green: Action = (element) => {
    element.style.color = "green";
  };

  const text: Action<HTMLElement, string> = (element, text) => {
    element.innerText = text;
  };
</script>

<h1 use:green>Heading</h1>

<p use:green use:text={"text"}></p>
