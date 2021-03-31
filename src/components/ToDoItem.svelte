<script>
  import { createEventDispatcher } from "svelte";
  const dispatch = createEventDispatcher();

  function advanceToDo(status) {
    dispatch("updateItemStatus", {
      newStatus: status === "to-do" ? "in-progress" : "complete"
    });
  }

  function revertToDo(status) {
    dispatch("updateItemStatus", {
      newStatus: status === "complete" ? "in-progress" : "to-do"
    });
  }

  export let itemText;
  export let dateCreated;
  export let status;
</script>

<div class="root">
  {itemText}
  <div>
    <caption>{dateCreated.toLocaleString()}</caption>
    <button
      on:click={() => revertToDo(status)}
      disabled={status === "to-do"}>{"<<"}</button
    >
    <button
      on:click={() => advanceToDo(status)}
      disabled={status === "complete"}>{">>"}</button
    >
  </div>
</div>

<style>
  .root {
    display: flex;
    margin: 0 0.2em 0.2em 0;
    align-items: baseline;
    justify-content: space-between;
  }

  caption {
    font-size: 10px;
  }
</style>
