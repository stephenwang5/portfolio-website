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
    tclas: ["software", "cloud", "Python", "Go", "JS", "TS", "C", "MQTT", "Svelte", "Express.js", "GCP", "VM", "Concurrency"],
    rtls: ["software", "Python", "Keras", "TensorFlow", "Bluetooth", "ML", "Deep Learning", "LSTM"],
    actionDetection: ["software", "Python", "C++", "ZMQ", "ML", "Deep Learning", "SlowFast", "Computer Vision", "GPU"],
    watcloud: ["cloud", "Linux", "Docker", "VM", "GPU", "Ansible", "Terraform"],
    milliOhmMeter: ["electrical", "KiCAD", "PCB"],
    switchBox: ["mechanical", "OnShape", "compliant"],
  };

  let disciplines = ["software", "cloud", "electrical", "mechanical"];

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
    tagHandler: addFilter,
    filter: [...filters],
  }

  $: tclasConf = {
    itemName: "TCLAS: Test Control, Logging, and Alert System",
    imagePath: "/electrans/diagram.png",
    tags: projectTags.tclas,
    ...summaryConf,
  }

  $: rtlsConf= {
    itemName: "RTLS: Real-Time Location Service",
    imagePath: "/rtls/screenshot.png",
    tags: projectTags.rtls,
    ...summaryConf,
  }

  $: actionDetectionConf = {
    itemName: "Violent Action Detection",
    imagePath: "/action-detection/bar.png",
    tags: projectTags.actionDetection,
    ...summaryConf,
  }

  $: watcloudConf = {
    itemName: "WATcloud Server Cluster",
    imagePath: "/watcloud/arch.png",
    tags: projectTags.watcloud,
    ...summaryConf,
  }

  $: milliohmMeterConf = {
    itemName: "Milliohm Meter",
    imagePath: "/milliohm/3d.png",
    tags: projectTags.milliOhmMeter,
    ...summaryConf,
  }

  $: switchBoxConf = {
    itemName: "Actuator Power Switch Box",
    imagePath: "/switch-box/box.png",
    tags: projectTags.switchBox,
    ...summaryConf,
  }
</script>

<body>

  <h1>Project List</h1>


  <div class="hori-flex center">
    Tags selected to filter:
    <div class="hori-flex filters user-selection">
      {#each [...filters] as f}
      <Tag {...selectedFilters} name={f} />
      {/each}
    </div>
    <button on:click={clearFilter}>Clear Tags</button>
  </div>

  <div class="hori-flex">
    <div class="filter-prompt">
      Disciplines
    </div>
    <div class="hori-flex filters">
      {#each disciplines as tag}
      <Tag {...availableFilters} name={tag} />
      {/each}
    </div>
  </div>

  <div class="hori-flex">
    <div class="filter-prompt">
      Buzz Words
    </div>
    <div class="hori-flex filters">
      {#each [...buzzwordSet] as tag}
      <Tag {...availableFilters} name={tag} />
      {/each}
    </div>
  </div>

  <SummaryItem {...tclasConf}>
    <p>I created a scalable IoT framework so that all test fixtures built for
      product durability testing can all be controlled, monitored, and logged
      in one place. This way, the control interface and logging peripherals
      don't need to be redesigned every time a new test fixture is built.
      Instead, the new fixture controller simply need to inherit the endpoint
      template and all other components will be automatically updated based
      on the new configuration.</p>
    <p>As shown in the architecture diagram on the left, the control interface
      web app, loggers, alert app, and the MQTT broker can all be deployed in
      Docker containers. That means this system can be hosted off-premise to a
      cloud provider like GCP for better uptime and reliability, or on-premise
      for better security.</p>
    <p>This system is a SCADA replacement for small enterprises and hobbyists
      who'd like to control and monitor numerous IoT devices at once without the
      counter-intuitive setup and overpriced licenses.</p>
  </SummaryItem>

  <SummaryItem {...rtlsConf}>
    <p>Localization in a GPS-denied indoor environment is tricky. Other forms of
      radio signal such as Bluetooth Low Energy (BLE) can be used to infer the
      location of the emitter instead. An Long-Short Term Memory neural network
      is used to make this inference.</p>
    <p>I made the data collection, training, and inference visualization parts
      of the ML pipeline. I wrote a modular model training script using Pandas
      for data preprocessing, Keras for model building, Numpy for postprocessing,
      and MLflow for experiment tracking. I created a full-stack visualizer for
      data collection and to debug the neural network and other parts of the
      inference pipeline because scalars and text don't tell the whole story.</p>
  </SummaryItem>

  <SummaryItem {...actionDetectionConf}>
    <p>Meta AI Research brought us SlowFast, a neural network architecture
      capable of predicting the action of actors in a video. I used their model
      to detect violent actions recorded in public spaces to more effectively
      monitor social discord.</p>
    <p>To facilitate neural network inference in real-time, I wrote a modular
      framework that allows serialized data to flow from sources through filters,
      then finally into sinks where the processed results are consumed. This
      framework also allows any node to be deployed onto any microprocessor so
      the whole system is platform-agnostic.
      Communication between these nodes was ZMQ's implementation of the router-dealer
      paradigm. This framework was implemented in Python. Processing nodes
      written this way can interoperate with existing nodes that were written in
      C++.</p>
  </SummaryItem>

  <SummaryItem {...watcloudConf}>
    <p><a href="https://watonomous.ca">WATonomous</a> is a student design team
      for self driving at the University of
      Waterloo. To meet the demanding simualtion workloads of the team, WATcloud
      server cluster was created to give software developers state-of-the-art
      consumer computer hardware so that they may start training models and
      running simulations as soon as they are onboarded.</p>
    <p>I maintained the infrastructure-as-code Ansible repository that provisions
      package installation and user management in Promox VMs. I frequently
      helped developers troubleshoot GPU and other resource usage problems
      and assembled a computer in the cluster. 10 gigabit networking runs between
      the cluster computers and I helped install a "big data" server that can be
      accessed anywhere in the cluster.</p>
  </SummaryItem>

  <SummaryItem {...milliohmMeterConf}>
    <p>To gauge how solid an electrical connection is, I designed a PCB that
      can measure resistance in the milliohm range. This PCB can measure 4
      connections simultaneously where each a known current is sunk through the
      connection, then the potential across the connection is amplified.</p>
    <p>A 23 pin connector is used because each measurement uses 4 wires so that
      the resistance of the wires connecting the milliohm meter to the
      connection under test would not affect the result.
    </p>
  </SummaryItem>

  <SummaryItem {...switchBoxConf}>
    <p>Two sources of input needed to be toggled for two linear actuators so I
      designed an easy-to-maintain box that would mount the DPDT switches.</p>
    <p>The lid of the box mates with the body using compliant clips so that no
      fastener, and hence no tool, is required to open or close the box in a
      pinch.</p>
  </SummaryItem>

</body>

<style>
  h1 {
    text-align: center;
  }
  p {
    font-stretch: condensed;
  }
  .user-selection {
    border: 2px;
    border-style: solid;
    border-color: rgb(103, 103, 103);
    border-radius: 12px;
    min-width: 40vw;
    min-height: 22px;
    margin-right: 6px;
    margin-left: 3px;
  }
  .hori-flex {
    display: flex;
    flex-wrap: wrap;
    flex-direction: row;
    align-items: center;
  }
  .center {
    justify-content: center;
  }
  .filters {
    flex-wrap: wrap;
    min-width: var(--mobile-min-width);
    max-width: 80vw;
    padding: 5px;
  }
  .filter-prompt {
    min-width: 120px;
  }
</style>
