<script>
  // Aquí puedes agregar lógica específica para el layout si es necesario
  import "../style.scss";
  import routes from "../lib/routes.json";
  import { page } from "$app/stores";
</script>

<nav>
  {#each routes as route}
    <a href={route.path} class:active={$page.url.pathname === route.path}
      >{route.name}</a
    >
  {/each}
</nav>

<main>
  <slot />
</main>

<style>
  nav {
    background: #333;
    padding: 1.3rem 2rem;
  }
  nav a {
    color: white;
    margin-right: 1.5rem;
    text-decoration: none;
  }
  main {
    padding: 2rem;
  }

  .active {
    text-decoration: underline;
  }

  /* :global(a) {
    color: blue;
  } */
</style>
