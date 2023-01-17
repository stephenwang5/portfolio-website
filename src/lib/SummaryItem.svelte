<script lang="ts">
  import Tag from "$lib/Tag.svelte";

  export let itemName : string;
  export let imagePath : string;
  export let tags : Array<string>;
  export let filter : Array<string>;
  export let tagHandler = (name: string) => {};

  let tagsSet = new Set(tags);
  tagsSet.add("");

  function shouldShow(selection: Array<string>): boolean {
    return selection.every(e => tagsSet.has(e));
  }
</script>

{#if shouldShow(filter)}

<div class="hori-flex summary">

  <img src={imagePath} alt={`${itemName} summary image`}/>

  <div>

    <h2>{itemName}</h2>

    <div class="content"><slot /></div>

    <div class="hori-flex tags">
      {#each tags as tag}
      <Tag name={tag} tagHandler={tagHandler}/>
      {/each}
    </div>

  </div>

</div>

{/if}

<style>
  img {
    width: 40vw;
    height: auto;
    padding: 12px;
  }
  h2, .content {
    width: 40vw;
  }
  .hori-flex {
    display: flex;
    flex-direction: row;
    align-items: center;
  }
  .summary{
    justify-content: center;
    margin-bottom: 20px;
  }
  .tags {
    flex-wrap: wrap;
    width: 30vw;
  }
</style>
