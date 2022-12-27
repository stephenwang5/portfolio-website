<script lang="ts">
  export let itemName : string;
  export let imagePath : string;
</script>

<div class="summary-item">
  <img src={imagePath} alt={`${itemName} summary image`}/>
  <div>
    <h2>{itemName}</h2>
    <slot />
  </div>
</div>

<style>
  img {
    width: 40%;
    padding: 12px;
  }
  .summary-item {
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;
  }
</style>
