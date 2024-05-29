<!-- components/BlogDetailPage.svelte -->

<script>
  import { page } from "$app/stores";
  import { onMount } from "svelte";
  import axios from "axios";

  let blog = {};

  onMount(async () => {
    const blogId = $page.params.id; // Obtiene el parámetro :id de la URL
    try {
      const res = await axios(
        `https://blog-6253e-default-rtdb.firebaseio.com/blog/${blogId}.json`
      );
      blog = res.data;
    } catch (error) {
      console.log(error);
    }
  });

  // get pathname
  let routeName;
  let cleanedRouteName;

  $: {
    $page.url.pathname;
    routeName = $page.url.pathname;
    cleanedRouteName = routeName.replace(/\//g, "-");
  }
  onMount(() => {
    routeName = $page.url.pathname;
    cleanedRouteName = routeName.replace(/\//g, "-");
    if (cleanedRouteName.startsWith("-")) {
      cleanedRouteName = cleanedRouteName.substring(1);
    }
  });
</script>

<section class="blog">
  <h2>Blog</h2>
  <h3 class="home-link">
    home/<a class="home-link" href="/blog">blogs</a>/{cleanedRouteName}
  </h3>
  <br />
  <br />
  <br />
  <br />
  <div class="blog__wrapper">
    <div class="blog__content-container">
      <div class="blog__image-container">
        <img src="/1.jpg" alt={blog.titulo} />
      </div>
      <div class="content-blog-container">
        {#if blog.titulo === undefined}
          <h1>Loading...</h1>
        {:else}
          <h1>{blog.titulo}</h1>
        {/if}
        {#if blog.titulo === undefined}
          <p>Loading...</p>
        {:else}
          <p>{blog.descripcion}</p>
        {/if}
      </div>
    </div>
  </div>
</section>

<style lang="scss">
  .blog {
    h2 {
      text-align: center;
      font-family: fantasy;
      font-size: 38px;
    }

    .blog__wrapper {
      width: 80%;
      margin: auto;

      .blog__content-container {
        display: grid;
        grid-template-columns: 35% 1fr;
        grid-column-gap: 20px;

        .blog__image-container {
          img {
            width: 100%;
          }
        }

        .content-blog-container {
          h1 {
            font-size: 24px;
          }

          p {
            font-size: 18px;
          }
        }
      }
    }
  }
</style>
