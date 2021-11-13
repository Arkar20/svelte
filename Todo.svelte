<script>
  import { createEventDispatcher } from "svelte";
  const dispatch = createEventDispatcher();
  export let todo = {};

  function handleRemove() {
    // dispatch an event

    dispatch("remove", {
      title: todo.title
    });
  }
</script>

<main>
  <li>{todo.title}
  <button on:click={handleRemove}>Remove</button>

  </li>
     

</main>