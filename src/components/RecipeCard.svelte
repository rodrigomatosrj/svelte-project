<script>
  import IconMeal from "./IconMeal.svelte";
  import IconKcal from "./IconKcal.svelte";
  export let recipeObj;

  $: recipe = recipeObj.recipe;
</script>

<div class="property-card">
  <a href="#/recipe/{recipe.uri.split('#')[1]}">
    <div class="property-image" style="background-image: url({recipe.image})" />
  </a>
  <div class="property-description">
    <h5>{recipe.label}</h5>
    <div class="meal-info">
      <IconKcal label={recipe.calories.toFixed(0)} />
      <IconMeal label={recipe.yield} />
    </div>
  </div>
</div>

<style>
  * {
    -webkit-box-sizing: border-box;
    box-sizing: border-box;
  }

  h5 {
    margin: 0px;
    font-size: 1.4em;
    font-weight: 700;
  }

  /* End Non-Essential  */

  .property-card {
    height: 18em;
    width: 300px;
    display: -webkit-box;
    display: -ms-flexbox;
    display: flex;
    -webkit-box-orient: vertical;
    -webkit-box-direction: normal;
    -ms-flex-direction: column;
    flex-direction: column;
    position: relative;
    -webkit-transition: all 0.4s cubic-bezier(0.645, 0.045, 0.355, 1);
    -o-transition: all 0.4s cubic-bezier(0.645, 0.045, 0.355, 1);
    transition: all 0.4s cubic-bezier(0.645, 0.045, 0.355, 1);
    border-radius: 16px;
    overflow: hidden;
    -webkit-box-shadow: 15px 15px 27px #e1e1e3, -15px -15px 27px #ffffff;
    box-shadow: 15px 15px 27px #e1e1e3, -15px -15px 27px #ffffff;
    margin: 20px;
  }
  /* ^-- The margin bottom is necessary for the drop shadow otherwise it gets clipped in certain cases. */

  /* Top Half of card, image. */

  .property-image {
    height: 6em;
    width: 300px;
    padding: 1em 2em;
    position: Absolute;
    top: 0px;
    -webkit-transition: all 0.4s cubic-bezier(0.645, 0.045, 0.355, 1);
    -o-transition: all 0.4s cubic-bezier(0.645, 0.045, 0.355, 1);
    transition: all 0.4s cubic-bezier(0.645, 0.045, 0.355, 1);
    background-size: cover;
    background-repeat: no-repeat;
  }

  /* Bottom Card Section */

  .property-description {
    background-color: #fafafc;
    height: 12em;
    width: 300px;
    position: absolute;
    bottom: 0em;
    -webkit-transition: all 0.4s cubic-bezier(0.645, 0.045, 0.355, 1);
    -o-transition: all 0.4s cubic-bezier(0.645, 0.045, 0.355, 1);
    transition: all 0.4s cubic-bezier(0.645, 0.045, 0.355, 1);
    padding: 0.5em 1em;
    text-align: center;
    display: flex;
    flex-direction: column;
    justify-content: space-evenly;
  }

  /* Property Cards Hover States */

  .property-card:hover .property-description {
    height: 0em;
    padding: 0px 1em;
  }
  .property-card:hover .property-image {
    height: 18em;
  }

  .property-card:hover {
    background-color: white;
  }

  .property-card:hover {
    cursor: pointer;
  }

  .meal-info {
    display: flex;
    align-items: center;
    justify-content: space-between;
  }
</style>
