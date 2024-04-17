<script lang="ts">
  import type { Action } from "svelte/action";
  import { spring } from "svelte/motion";

  const followCursor: Action = (element) => {
    window.addEventListener("mousemove", (event) => {
      const elementHalfHeight =
        Number(getComputedStyle(element).height.replace("px", "") ?? 0) / 2;
      element.style.top = `${event.clientY - elementHalfHeight}px`;

      const elementHalfWidth =
        Number(getComputedStyle(element).width.replace("px", "") ?? 0) / 2;
      element.style.left = `${event.clientX - elementHalfWidth}px`;
    });
  };

  const followCursorSpring: Action = (element) => {
    // Spring is a special store that eases the values that
    // are set to it, instead of instantly setting them
    let elementTop = spring(0, {
      damping: 0.6,
      precision: 0.5,
      stiffness: 0.2,
    });
    let elementLeft = spring(0, {
      damping: 0.6,
      precision: 0.5,
      stiffness: 0.2,
    });

    window.addEventListener("mousemove", (event) => {
      elementTop.set(event.clientY);
      elementLeft.set(event.clientX);
    });

    elementTop.subscribe((top) => {
      const elementHalfHeight =
        Number(getComputedStyle(element).height.replace("px", "") ?? 0) / 2;
      element.style.top = `${top - elementHalfHeight}px`;
    });

    elementLeft.subscribe((left) => {
      const elementHalfWidth =
        Number(getComputedStyle(element).width.replace("px", "") ?? 0) / 2;
      element.style.left = `${left - elementHalfWidth}px`;
    });
  };
</script>

<h1>Cursor Events</h1>

<div use:followCursor></div>

<div use:followCursorSpring class="green"></div>

<style>
  div {
    position: absolute;
    background-color: royalblue;
    width: 100px;
    height: 100px;
    border-radius: 100px;
  }

  div.green {
    background-color: greenyellow;
    width: 50px;
    height: 50px;
  }
</style>
