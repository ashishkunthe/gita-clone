<script>
  import Router from "svelte-spa-router";

  import ChaptersPage from "./pages/ChapterPage.svelte";
  import Gita from "./pages/Gita.svelte";

  const routes = {
    "/": ChaptersPage,
    "/chapter/:chapter": Gita
  };
</script>

<Router {routes} />

<style>
  :global(body) { margin: 0; }
</style>
