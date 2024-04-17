<section class="app">
  <slot />
</section>

<section class="links">
  <a href="/">Home</a>
  <a href="/basic">Basic</a>
  <a href="/cursor-events">Cursor Events</a>
  <a href="/update">Update</a>
  <a href="/destroy">Destroy</a>
  <a href="/tooltip">Tooltip</a>
</section>

<style>
  .app {
    flex: 1;
  }

  .links {
    padding: 1rem;
  }

  :global(body) {
    margin: 0;
    display: flex;
    flex-direction: column;
    height: 100vh;
  }
</style>
