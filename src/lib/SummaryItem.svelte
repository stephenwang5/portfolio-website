<script lang="ts">
  export let itemName : string;
  export let imagePath : string;
</script>

<h3>{itemName}</h3>

<img src={imagePath} alt={`${itemName} summary image`}/>


