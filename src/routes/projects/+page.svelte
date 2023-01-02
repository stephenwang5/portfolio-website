<script lang="ts">
  import SummaryItem from "$lib/SummaryItem.svelte";
  import Tag from "$lib/Tag.svelte";

  let filter = Array(10);

  let filterConf = {
    clickHandler: debugHandler,
    withDismiss: true,
  }

  function handler() {
    filter[0] = "";
    filter[1] = "";
  }
  function debugHandler() {
    console.log("clicked!");
  }
</script>

<body>
  <h1>Software</h1>

  <select bind:value={filter[0]}>
    <option value="software">Software</option>
    <option value="electrical">Electrical</option>
    <option value="mechanical">Mechanical</option>
  </select>

  <select bind:value={filter[1]}>
    <option value="software">Software</option>
    <option value="electrical">Electrical</option>
    <option value="mechanical">Mechanical</option>
  </select>

  <button on:click={handler}>RESET</button>

  <div id="filters">
    <Tag {...filterConf} name="software" />
    <Tag {...filterConf} name="electrical" />
    <Tag {...filterConf} name="mechanical" />
    <Tag {...filterConf} name="ai" />
    <Tag {...filterConf} name="computer vision" />
  </div>

  <SummaryItem itemName="TCLAS" imagePath="electrans/diagram.png"
    filter={filter}
    tags={["software"]}>
    <p>sdfhklsdflkjsldjkf</p>
  </SummaryItem>

  <SummaryItem itemName="Mech TCLAS" imagePath="electrans/diagram.png"
    filter={filter}
    tags={["mechanical"]}>
    <p>sdfhklsdflkjsldjkf</p>
  </SummaryItem>

  <SummaryItem itemName="Mech ECE TCLAS" imagePath="electrans/diagram.png"
    filter={filter}
    tags={["electrical", "mechanical"]}>
    <p>sdfhklsdflkjsldjkf>
  </SummaryItem>

  <SummaryItem itemName="ECE TCLAS" imagePath="electrans/diagram.png"
    filter={filter}
    tags={["electrical"]}>
    <p>sdfhklsdflkjsldjkf</p>
  </SummaryItem>

</body>

<style>
  h1 {
    text-align: center;
  }
  #filters {
    display: flex;
    flex-direction: row;
    padding-top: 10px;
    padding-bottom: 16px;
  }
</style>
