<script lang="ts">
  import NavBar from "./NavBar.svelte";
  import "./FontSettings.css";
</script>

<svelte:head>
  <title>Stephen Wang</title>
</svelte:head>

<a href="https://sxwang.dev">
  <h1>Stephen Xiren Wang</h1>
</a>

<NavBar />

<slot />

<style>
  h1 {
    text-align: center;
  }
</style>
