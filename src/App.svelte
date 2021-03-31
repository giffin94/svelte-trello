<script>
  import ItemInput from "./components/ItemInput.svelte";
  import ToDoItem from "./components/ToDoItem.svelte";

  let currentUser = false;

  let allItems = [
    { id: 0, text: "See a movie", dateCreated: new Date(), status: "to-do" },
    {
      id: 1,
      text: "Take a walk",
      dateCreated: new Date(),
      status: "in-progress",
    },
    { id: 2, text: "Go to the park", dateCreated: new Date(), status: "to-do" },
    { id: 3, text: "Make Dinner", dateCreated: new Date(), status: "to-do" },
    { id: 4, text: "Send email", dateCreated: new Date(), status: "complete" },
  ];

  $: toDoItems = [...allItems].filter(({ status }) => status === "to-do");

  $: inProgressItems = [...allItems].filter(
    ({ status }) => status === "in-progress"
  );
  $: completedItems = [...allItems].filter(
    ({ status }) => status === "complete"
  );

  function handleNewItem(event) {
    toDoItems = [...toDoItems, event.detail.item];
    console.log(event.detail.item);
  }

  function handleUpdateItemStatus(event, id) {
    const newStatus = event.detail.newStatus;
    const foundIndex = allItems.findIndex((el) => el.id === id);
    console.log(newStatus);
    if (foundIndex !== -1) {
      allItems[foundIndex].status = newStatus;
    }
  }
</script>

{#if currentUser}
  <ItemInput on:newItem={handleNewItem} />
  {#if toDoItems.length}
    <p>To Do:</p>
  {/if}
  <ul>
    {#each toDoItems as { id, text, dateCreated, status } (id)}
      <ToDoItem
        on:updateItemStatus={(e) => handleUpdateItemStatus(e, id)}
        itemText={text}
        {dateCreated}
        {status}
      />
    {/each}
  </ul>

  {#if inProgressItems.length}
    <p>In Progress:</p>
  {/if}

  <ul>
    {#each inProgressItems as { id, text, dateCreated, status } (id)}
      <ToDoItem
        on:updateItemStatus={(e) => handleUpdateItemStatus(e, id)}
        itemText={text}
        {dateCreated}
        {status}
      />
    {/each}
  </ul>

  {#if completedItems.length}
    <p>Complete:</p>
  {/if}

  <ul>
    {#each completedItems as { id, text, dateCreated, status } (id)}
      <ToDoItem
        on:updateItemStatus={(e) => handleUpdateItemStatus(e, id)}
        itemText={text}
        {dateCreated}
        {status}
      />
    {/each}
  </ul>
  <button on:click={() => (currentUser = false)}>LOG OUT</button>
{:else}
  <button on:click={() => (currentUser = true)}>LOG IN</button>
{/if}
