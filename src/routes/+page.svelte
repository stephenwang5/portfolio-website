<script lang="ts">
  import { fly } from "svelte/transition";
  import { onMount } from "svelte";

  let started = false;

  onMount(() => {
    started = true;
  });
</script>

<div id="body">

  <div id="intro">

    {#if started}
    <img in:fly={{ x: -50, duration: 700 }}
      src="headshot.jpeg" alt="My profile pic"/>

    <div in:fly={{ x: 50, duration: 700 }}
      id="greeting">
      <h1>Hi! I'm Xiren.</h1>
      <h1>You can call me Stephen.</h1>
    </div>
    {/if}

  </div>

  <p>
    I'm a graduating Mechatronics Engineering student at the University of Waterloo
  </p>

  <p>
    I love IoT, robotics, and deep learning :D
  </p>

</div>

<style>
  #body {
    display: flex;
    flex-direction: column;
    text-align: center;
    height: 80vh;
    justify-content: space-evenly;
  }
  #intro {
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;
  }
  #greeting {
    text-align: left;
    padding-left: 20px;
  }
  #intro img {
    width: 30%;
  }
</style>
