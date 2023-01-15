<script lang="ts">
  import SummaryItem from "$lib/SummaryItem.svelte";
  import Tag from "$lib/Tag.svelte";

  let filters : Set<string> = new Set();

  function addFilter(name: string) {
    filters = filters.add(name);
  }

  function rmFilter(name: string) {
    filters.delete(name);
    filters = filters;
  }

  function clearFilter(e: MouseEvent) {
    filters = new Set();
  }

  let projectTags = {
    tclas: ["software"],
    mechTclas: ["mechanical"],
    mechEceTclas: ["electrical", "mechanical", "bleh", "blah", "hmmmm", "bruhhh"],
    eceTclas: ["electrical"],
  };

  let disciplines = ["software", "electrical", "mechanical"];

  let buzzwordList = Object.entries(projectTags).reduce((acc, cur) =>
    acc.concat(cur[1]), new Array());
  let buzzwordSet = new Set(buzzwordList);
  disciplines.forEach(d => buzzwordSet.delete(d));

  let availableFilters = {
    tagHandler: addFilter,
  }

  let selectedFilters = {
    withDismiss: true,
    dismissHandler: rmFilter,
  }

  $: summaryConf = {
    imagePath: "electrans/diagram.png",
    tagHandler: addFilter,
    filter: [...filters],
  }

  $: tclasConf = {
    itemName: "TCLAS",
    tags: projectTags.tclas,
    ...summaryConf,
  }

  $: mechTclasConf = {
    itemName: "Mech TCLAS",
    tags: projectTags.mechTclas,
    ...summaryConf,
  }

  $: mechEceTclasConf = {
    itemName: "Mech ECE TCLAS",
    tags: projectTags.mechEceTclas,
    ...summaryConf,
  }

  $: eceTclasConf = {
    itemName: "ECE TCLAS",
    tags: projectTags.eceTclas,
    ...summaryConf,
  }
</script>

<body>

  <h1>Project List</h1>

  <button on:click={clearFilter}>Clear Tags</button>

  <div class="hori-flex filters">
    {#each [...filters] as f}
    <Tag {...selectedFilters} name={f} />
    {/each}
  </div>

  <div class="hori-flex">
    Disciplines
    <div class="hori-flex filters">
      {#each disciplines as tag}
      <Tag {...availableFilters} name={tag} />
      {/each}
    </div>
  </div>

  <div class="hori-flex">
    Buzz Words
    <div class="hori-flex filters">
      {#each [...buzzwordSet] as tag}
      <Tag {...availableFilters} name={tag} />
      {/each}
    </div>
  </div>

  <SummaryItem {...tclasConf}>
    <p>sdfhklsdflkjsldjkf</p>
  </SummaryItem>

  <SummaryItem {...mechTclasConf}>
    <p>sdfhklsdflkjsldjkf</p>
  </SummaryItem>

  <SummaryItem {...mechEceTclasConf}>
    <p>sdfhklsdflkjsldjkf</p>
  </SummaryItem>

  <SummaryItem {...eceTclasConf}>
    <p>sdfhklsdflkjsldjkf</p>
  </SummaryItem>

</body>

<style>
  h1 {
    text-align: center;
  }
  .hori-flex {
    display: flex;
    flex-direction: row;
    align-items: center;
  }
  .filters {
    flex-wrap: wrap;
    padding: 5px;
  }
</style>
