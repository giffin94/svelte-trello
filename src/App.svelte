<script>
  import ItemInput from "./components/ItemInput.svelte";
  import ToDoItem from "./components/ToDoItem.svelte";

  let toDoItems = [
    { text: "See a movie", dateCreated: Date.now(), status: "to-do" },
    { text: "Take a walk", dateCreated: Date.now(), status: "to-do" },
    { text: "Go to the park", dateCreated: Date.now(), status: "to-do" },
    { text: "Make Dinner", dateCreated: Date.now(), status: "to-do" },
    { text: "Send email", dateCreated: Date.now(), status: "to-do" },
  ];

  function handleNewItem(event) {
    toDoItems = [...toDoItems, event.detail.item];
    console.log(event.detail.item)
  }
</script>

<h1>
  <ItemInput on:newItem={handleNewItem} />

  <ul>
    {#each toDoItems as { text, dateCreated, status }}
      <ToDoItem itemText={text} {dateCreated} />
    {/each}
  </ul>
</h1>
