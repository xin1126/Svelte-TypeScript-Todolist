<script lang="ts">
  import { Router } from "svelte-router-spa";
  import { routes } from "./router/index";
</script>

<main>
  <Router {routes} />
</main>
