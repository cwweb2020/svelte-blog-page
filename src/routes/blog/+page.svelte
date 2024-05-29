<!-- BlogPage.svelte -->

<script>
  import { page } from "$app/stores";
  import { onMount } from "svelte";

  // Datos de los blogs (ejemplo)
  const blogs = [
    {
      id: 1,
      title: "Título del Blog 1",
      text: "Contenido del Blog 1...",
      imageUrl: "url_de_la_imagen_1.jpg",
    },
    {
      id: 2,
      title: "Título del Blog 2",
      text: "Contenido del Blog 2...",
      imageUrl: "url_de_la_imagen_2.jpg",
    },
    // Agregar más blogs según sea necesario
  ];

  let routeName;
  let cleanedRouteName;

  $: {
    $page.url.pathname;
    routeName = $page.url.pathname;
    cleanedRouteName = routeName.replace(/\//g, "");
  }

  onMount(() => {
    routeName = $page.url.pathname;
    cleanedRouteName = routeName.replace(/\//g, "");
  });
</script>

<h1>Últimos Blogs</h1>

<br />
<h3><a class="home-link" href="/">home</a>/{cleanedRouteName}</h3>
<br />
<br />
<br />

<div class="container">
  {#each blogs as blog}
    <div class="blog-container">
      <img src="/1.jpg" alt={blog.title} class="blog-image" />
      <div class="blog-content">
        <h2 class="blog-title">{blog.title}</h2>
        <p class="blog-text">{blog.text}</p>
      </div>
    </div>
  {/each}
</div>

<style lang="scss">
  .blog-container {
    display: flex;
    align-items: center;
    margin-bottom: 20px;
  }

  .blog-image {
    width: 250px;
    height: auto;
    margin-right: 20px;
  }

  .blog-title {
    font-size: 1.5rem;
    margin-bottom: 10px;
  }

  .blog-text {
    font-size: 1rem;
  }

  h1 {
    font-family: fantasy;
    text-align: center;
  }

  .home-link {
    background: tan;
  }
  h3 {
    font-size: 18px;
  }
  .container {
    margin: 0 40px;
  }

  :global(.global-class) {
    color: red;
  }
</style>
