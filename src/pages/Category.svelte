<script>
  import { onMount } from "svelte";
  import axios from "axios";
  import RecipeCard from "../components/RecipeCard.svelte";
  import Loading from "../components/Loading.svelte";

  export let params;
  let category = params.categoryName;

  $: recipes = [];
  $: page = 1;

  async function fetchData() {
    try {
      const res = await axios.get("https://api.edamam.com/search", {
        params: {
          q: category,
          app_id: "21e55cbb",
          app_key: "7997ac895e74b2bee7c28adf23b50038",
          from: (page - 1) * 10,
          to: page * 10,
        },
      });
      recipes = res.data.hits;
    } catch (e) {
      console.error(e);
    }
  }

  function goFoward() {
    page++;
    fetchData();
  }

  function goBackward() {
    page--;
    fetchData();
  }

  onMount(fetchData);
</script>

<div class="flex-container">
  {#if recipes.length > 0}
    {#each recipes as recipe}
      <RecipeCard recipeObj={{ ...recipe }} />
    {/each}
    <div class="pagination">
      {#if page > 1}
        <button on:click={goBackward}>Página Anterior</button>
      {/if}
      <button on:click={goFoward}>Próxima Página</button>
    </div>
  {:else}
    <Loading />
  {/if}
</div>

<style>
  .pagination {
    width: 100%;
  }

  .flex-container {
    display: flex;
    flex-wrap: wrap;
    width: 100%;
    height: 100vh;
    align-items: center;
    flex-direction: column;
    justify-content: space-evenly;
    background-color: #fff;
    align-self: center;
  }

  @media only screen and (min-width: 576px) {
    .flex-container {
      justify-content: space-evenly;
      flex-direction: row;
      align-items: flex-start;
    }
  }
</style>
