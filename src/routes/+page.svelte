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
    showBreaks = window.innerWidth >= 900;
  };
  // console.log(city);

  let data;
  let loading = true;
  let algo = true;
  onMount(async () => {
    window.addEventListener("resize", updateShowBreaks);
    updateShowBreaks();
    try {
      const res = await axios(`https://jsonplaceholder.typicode.com/comments/`);
      data = res.data;
      let halfLength = Math.ceil(data.length / 70);
      data = data.slice(0, halfLength);

      // console.log(data);
    } catch (error) {
      console.log(error);
    } finally {
      loading = false;
    }
  });
  // console.log(loading);
</script>

<h1>Lista de blogs</h1>

{#if showBreaks}
  <br />
  <br />
  <br />
{/if}
{#if loading}
  <p class="loading">loading...</p>
{:else}
  <img src="/1.jpg" alt="" />
  <ul>
    {#each data as { name, body }}
      <li>
        <h3><strong>{name}</strong></h3>
      </li>

      <p class:normal={!algo} class:inactive={algo}>{body}</p>
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
    font-size: 18px;
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
