<!-- BlogPage.svelte -->

<script>
  import { page } from "$app/stores";
  import { onMount } from "svelte";
  import axios from "axios";
  import { goto } from "$app/navigation";

  let showBreaks;
  const updateShowBreaks = () => {
    showBreaks = window.innerWidth < 900;
  };
  // Datos de los blogs
  let data = [];
  let loading = true;

  onMount(async () => {
    window.addEventListener("resize", updateShowBreaks);
    updateShowBreaks();
    try {
      const res = await axios(
        `https://blog-6253e-default-rtdb.firebaseio.com/blog.json`
      );
      data = Object.keys(res.data).map((id) => ({
        id,
        ...res.data[id],
      }));

      // console.log(data);
    } catch (error) {
      console.log(error);
    } finally {
      loading = false;
    }
  });

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

  function goToBlog(id) {
    goto(`/blog/${id}`);
  }
</script>

<h1>Últimos Blogs</h1>

<br />
<h3><a class="home-link" href="/">home</a>/{cleanedRouteName}</h3>
<br />
<br />
<br />

<div class="container">
  {#if loading}
    <h3 class="loading">loading...</h3>
  {/if}
  {#each data as { titulo, descripcion, id }}
    <div class="blog-container" on:click={() => goToBlog(id)}>
      {#if titulo !== undefined}
        <img src="/1.jpg" alt={titulo} class="blog-image" />
      {/if}
      <div class="blog-content">
        <h2 class="blog-title">
          {#if titulo !== undefined}{titulo}{/if}
        </h2>
        <p class="blog-text">
          {#if titulo !== undefined}{descripcion}{/if}
        </p>
      </div>
    </div>
  {/each}
</div>

<style lang="scss">
  .blog-container {
    display: flex;
    align-items: center;
    margin-bottom: 20px;
    cursor: pointer;
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
  .loading {
    font-size: 23px;
    font-family: monospace;
    text-transform: capitalize;
  }
</style>
