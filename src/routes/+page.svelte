<script>
  import axios from "axios";
  import { onMount } from "svelte";

  let person = {
    firstName: "John",
    lastName: "Doe",
    address: {
      street: "123 Main St",
      city: "Anytown",
    },
  };

  const {
    firstName,
    lastName,
    address: { city },
  } = person;

  let showBreaks;
  const updateShowBreaks = () => {
    showBreaks = window.innerWidth < 900;
  };
  // console.log(city);

  let data = [];
  let loading = true;
  let algo = true;
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
  // console.log(loading);
</script>

<h1>Bienvenidos a mi blog</h1>

{#if !showBreaks}
  <br />
  <br />
  <br />
{/if}
{#if loading}
  <h3 class="loading">loading...</h3>
{:else if data.length > 0}
  <img src="/1.jpg" alt="" />
  <ul>
    {#each data as { titulo, descripcion }}
      <li>
        <h3>
          {#if titulo !== undefined}<strong>{titulo}</strong>{/if}
        </h3>
      </li>

      <p class:normal={!algo} class:inactive={algo}>
        {#if titulo !== undefined}{descripcion}{/if}
      </p>
    {/each}
  </ul>
{/if}

<style>
  ul {
    list-style: none;
  }
  h1 {
    font-family: fantasy;
    text-align: center;
  }
  p {
    font-family: monospace;
    font-size: 18px;
    width: 90%;
  }

  h3 {
    /* margin-bottom: 8px; */
    font-size: 22px;
    font-family: monospace;
    text-transform: capitalize;
  }
  .loading {
    font-size: 23px;
    font-family: monospace;
    text-transform: capitalize;
  }

  span {
    font-family: monospace;
    font-size: 18px;
  }
  img {
    width: 458px;
    margin-left: 50px;
    float: left;
    margin-right: 20px;
    margin-bottom: 5px;
  }

  .normal {
    color: red;
  }
  .inactive {
    color: rgb(51, 68, 69);
  }
  .ir-button {
    background: white;
    font-size: 17px;
    padding: 5px 12px;
    text-decoration: none;
    text-transform: capitalize;
    border-radius: 8px;
  }
</style>
