<script lang="ts">
  import type { Component } from "svelte";
  import Home from "./pages/Home.svelte";
  import Review from "./pages/Review.svelte";

  const routes: Record<string, Component> = {
    "/": Home,
    "/review": Review,
  };

  function getCurrentRoute(): string {
    let path = location.hash.slice(1) || "/";
    console.log(path);
    return path;
  }

  function navigateTo(route: string) {
    location.hash = route;
  }

  let route = $state(getCurrentRoute());
  let Page = $derived(routes[route] ?? Home);
</script>

<svelte:window on:hashchange={() => (route = getCurrentRoute())} />

<Page />
