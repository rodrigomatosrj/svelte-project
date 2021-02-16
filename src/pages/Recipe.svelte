<script>
  import { onMount } from "svelte";
  import axios from "axios";
  import IconMeal from "../components/IconMeal.svelte";
  import IconKcal from "../components/IconKcal.svelte";
  import Loading from "../components/Loading.svelte";

  export let params;
  let recipes = [];

  onMount(async () => {
    try {
      const res = await axios.get("https://api.edamam.com/search", {
        params: {
          r: "http://www.edamam.com/ontologies/edamam.owl#" + params.recipeId,
          app_id: "21e55cbb",
          app_key: "7997ac895e74b2bee7c28adf23b50038",
        },
      });
      recipes = res.data;
    } catch (e) {
      console.error(e);
    }
  });
</script>

{#if recipes.length > 0}
  {#each recipes as recipe}
    <div class="recipe">
      <div class="div-image" style="background-image: url({recipe.image})">
        &nbsp;
      </div>
      <div>
        <h1>{recipe.label}</h1>
        Ingredients
        <ul>
          {#each recipe.ingredientLines as ingredientLine}
            <li>{ingredientLine}</li>
          {/each}
        </ul>
        <div class="div-icons">
          <IconKcal label={recipe.calories.toFixed(0)} />
          <IconMeal label={recipe.yield} />
        </div>
      </div>
    </div>
  {/each}
{:else}
  <Loading />
{/if}

<style>
  .div-icons {
    width: 100%;
    display: flex;
    justify-content: space-around;
  }
  .recipe {
    display: flex;
    width: 100%;
    align-items: center;
    flex-direction: column;
    justify-content: space-evenly;
    background-color: #fff;
    align-self: center;
    padding-bottom: 20px;
  }

  @media only screen and (min-width: 576px) {
    .recipe {
      justify-content: space-evenly;
      flex-direction: row;
      align-items: flex-start;
    }
  }

  .div-image {
    width: 300px;
    height: 300px;
    background-size: center;
    background-repeat: no-repeat;
    margin-top: 20px;
  }

  li {
    list-style-type: none;
    padding: 5px;
  }
</style>
