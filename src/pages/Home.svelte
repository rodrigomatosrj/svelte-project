<script>
  import IconCategory from "../components/IconCategory.svelte";
</script>

<div>
  <IconCategory category="chicken" />
  <IconCategory category="meat" />
  <IconCategory category="pasta" />
  <IconCategory category="fish" />
</div>

<style>
  div  {
    width: 100%;
    display: flex;
    justify-content: space-evenly;
  }
</style>