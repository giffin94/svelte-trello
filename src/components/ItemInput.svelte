<script>
  import { createEventDispatcher } from "svelte";
  import { v4 as uuidv4 } from "uuid";

  const dispatch = createEventDispatcher();

  let newToDo = "";

  function createToDo() {
    dispatch("newItem", {
      item: { id: uuidv4(), text: newToDo, dateCreated: new Date(), status: "to-do" },
    });
  }
</script>

Enter To-Do: <input
  on:input={(e) => (newToDo = e.currentTarget.value)}
  type="text"
  value={newToDo}
/>
<button on:click={createToDo}>Create</button>
