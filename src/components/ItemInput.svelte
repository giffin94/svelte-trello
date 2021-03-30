<script>
  import { createEventDispatcher } from "svelte";

  const dispatch = createEventDispatcher();

  let newToDo = '';

  function createToDo() {
    dispatch("newItem", {
      item: { text: newToDo, dateCreated: Date.now(), status: "to-do" },
    });
  }
</script>

Enter To-Do: <input
  on:input={(e) => (newToDo = e.currentTarget.value)}
  type="text"
  value={newToDo}
/>
<button on:click={createToDo}>asdghkjd</button>
