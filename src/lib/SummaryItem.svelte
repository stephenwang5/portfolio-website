<script lang="ts">
  import Tag from "$lib/Tag.svelte";

  export let itemName : string;
  export let imagePath : string;
  export let tags : Array<string>;
  export let filter : Array<string>;

  let tagsSet = new Set(tags);
  tagsSet.add("");

  function shouldShow(selection: Array<string>): boolean {
    return selection.every(e => tagsSet.has(e));
  }
</script>

{#if shouldShow(filter)}

<div class="summary-item">

  <img src={imagePath} alt={`${itemName} summary image`}/>

  <div>

    <h2>{itemName}</h2>

    <slot />

    {#each tags as tag}
    <Tag name={tag} />
    {/each}

  </div>

</div>

{/if}

<style>
  img {
    width: 40%;
    padding: 12px;
  }
  .summary-item {
    display: flex;
    flex-direction: row;
    justify-content: center;
  }
</style>
