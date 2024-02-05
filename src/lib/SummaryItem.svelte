<script lang="ts">
  import Tag from "$lib/Tag.svelte";

  export let itemName : string;
  export let imagePath : string;
  export let videoURL : string;
  export let height : string = "auto";
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

<div class="hori-flex summary" style="--height:{height}">

  {#if imagePath}
    <img src={imagePath} alt={`${itemName} summary image`}/>
  {:else if videoURL}
    <iframe src={videoURL} title={`${itemName} summary video`}></iframe>
  {/if}

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
  :root {
    --mobile-min-width: 300px;
  }
  img {
    width: 40vw;
    min-width: var(--mobile-min-width);
    max-width: 700px;
    height: auto;
    padding: 12px;
    margin-right: 3vw;
  }
  iframe {
    width: 40vw;
    /* min-width: var(--mobile-min-width); */
    /* max-width: 700px; */
    /* max-height: 30vh; */
    height: var(--height);
    margin-right: 3vw;
    margin-left: 24px;
  }
  h2, .content {
    width: 40vw;
    min-width: var(--mobile-min-width);
  }
  .hori-flex {
    display: flex;
    flex-wrap: wrap;
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
    min-width: var(--mobile-min-width);
  }
</style>
