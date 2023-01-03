<script lang="ts">
  import Cross from "./Cross.svelte";

  export let name : string;
  export let tagHandler = (name: string) => {};

  export let withDismiss : boolean = false;
  export let dismissHandler = (name: string) => {};

  function tagClick(e: MouseEvent) {
    tagHandler(name);
  }

  function dismiss(e: MouseEvent) {
    dismissHandler(name);
  }
</script>

<div class="container">

  {#if !withDismiss}
  <button class="btn tag" on:click={tagClick}> #{name} </button>
  {/if}

  {#if withDismiss}
  <div class="no-space">
    <button class="btn tag-dismiss" on:click={tagClick}> #{name} </button>
    <button class="btn dismiss" on:click={dismiss}><Cross /></button>
  </div>
  {/if}

</div>

<style lang="scss">
  $bgcolor: rgb(255, 225, 225);
  $txtcolor: rgb(141, 141, 141);

  .container {
    padding-right: 4px;
    padding-top: 2px;
    padding-bottom: 2px;
    display: flex;
    flex-direction: row;
  }

  .btn {
    background-color: $bgcolor;
    transition: background-color 0.1s ease;
    color: $txtcolor;
    display: inline-block;
    border-radius: 8px;
    cursor: pointer;
    border-style: none;
    margin: 0; // for safari

    &:hover {
      background-color: darken($bgcolor, 5);
    }

    &:active {
      color: #e2e2e2;
      background-color: darken($bgcolor, 10);
    }
  }

  .tag {
    padding-left: 5px;
    padding-right: 5px;
  }

  .tag-dismiss {
    border-top-right-radius: 0;
    border-bottom-right-radius: 0;
    padding-right: 0;
    margin: 0;
  }

  .dismiss {
    margin: 0;
    border-top-left-radius: 0;
    border-bottom-left-radius: 0;
    padding-top: 0;
    padding-bottom: 0;
    height: 100%;
  }

  .no-space {
    display: inline-flex;
  }
</style>
