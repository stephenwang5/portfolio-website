<script lang="ts">
  import Cross from "./Cross.svelte";

  export let name : string;
  export let clickHandler = () => {};

  export let withDismiss : boolean = false;
  export let dismissHandler = () => {};
</script>

<div class="container">

  {#if !withDismiss}
  <button class="btn tag" on:click={clickHandler}> #{name} </button>
  {/if}

  {#if withDismiss}
  <div class="no-space">
    <button class="btn tag-dismiss" on:click={clickHandler}> #{name} </button>
  </div>
  <div class="no-space">
    <button class="btn dismiss" on:click={dismissHandler}><Cross /></button>
  </div>
  {/if}

</div>

<style lang="scss">
  $bgcolor: rgb(255, 225, 225);
  $txtcolor: rgb(141, 141, 141);

  .btn{
    background-color: $bgcolor;
    transition: background-color 0.1s ease;
    color: $txtcolor;
    display: inline-block;
    border-radius: 8px;
    cursor: pointer;
    border-style: none;

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
  }

  .dismiss {
    border-top-left-radius: 0;
    border-bottom-left-radius: 0;
  }

  .no-space {
    font-size: 0;
  }

  .container {
    padding-right: 4px;
    padding-top: 2px;
    padding-bottom: 2px;
    display: flex;
    flex-direction: row;
  }
</style>
