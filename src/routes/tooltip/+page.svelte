<script lang="ts">
  import type { Action } from "svelte/action";

  const tooltip: Action<HTMLElement, { content: string }> = (node, options) => {
    let id = crypto.randomUUID();

    let showing = false;

    node.addEventListener("mouseover", (event) => {
      if (showing) {
        return;
      }

      showing = true;

      const tooltipWrapper = document.createElement("div");
      tooltipWrapper.style.position = "relative";
      tooltipWrapper.style.display = "flex";
      tooltipWrapper.style.alignItems = "center";
      tooltipWrapper.style.width = "100%";
      tooltipWrapper.style.height = "100%";

      tooltipWrapper.id = id;

      const tooltipContainer = document.createElement("span");
      tooltipContainer.style.position = "absolute";
      tooltipContainer.style.top = "16px";
      tooltipContainer.style.background = "lightgrey";
      tooltipContainer.style.padding = "4px";

      tooltipContainer.innerText = options.content;

      tooltipWrapper.appendChild(tooltipContainer);

      node.appendChild(tooltipWrapper);
    });

    node.addEventListener("mouseleave", (event) => {
      if (!showing) {
        return;
      }

      showing = false;

      const tooltipWrapper = document.getElementById(id);

      if (!tooltipWrapper) {
        return;
      }

      node.removeChild(tooltipWrapper);
    });
  };
</script>

<h1>Tooltip Example</h1>

<button use:tooltip={{ content: "I'm a tooltip!" }}>Hover over me!</button>

<!-- It even works with multiple! -->
<button use:tooltip={{ content: "I'm a tooltip in the second one!" }}>
  Hover over second!
</button>

<button use:tooltip={{ content: "I'm a tooltip in the third one!" }}>
  Hover over third!
</button>
