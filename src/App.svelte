<script>
  import Home from "./pages/Home.svelte";
  import Recipe from "./pages/Recipe.svelte";
  import Router from "svelte-spa-router";
  import Category from "./pages/Category.svelte";

  const routes = {
    "/": Home,
    "/category/:categoryName/:page": Category,
    "/category/:categoryName": Category,
    "/recipe/:recipeId": Recipe
  };
</script>

<main>
  <Router {routes} />
</main>

<style>
  main {
    width: 100%;
    font-size: 10px;
    background-color: #fff;
    transition: 1s;
  }

  @media only screen and (min-width: 576px) {
    main {
      width: 90%;
      font-size: 12px;
      margin: 0 5% 0 5%;
    }
  }
</style>
