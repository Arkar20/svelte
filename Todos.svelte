<script>
  import { onMount } from "svelte";
  import Todo from "./Todo";

  let task = "";
  let todos = [];

  onMount(() => {
    fetch("https://jsonplaceholder.typicode.com/todos")
      .then(res => res.json())
      .then(data => (todos = data));
  });

  function handleSubmit() {
    todos = [{ title: task, completed: false }, ...todos];
    task = "";
  }

  function handleRemove(e) {
    todos = todos.filter(todo => todo.title !== e.detail.title);
  }
  function handleFilterComplete() {
    todos = todos.filter(todo => todo.completed);
  }
</script>

<main>
 <form on:submit|preventDefault={handleSubmit}>
      <input type="text" bind:value={task}>
  </form>
  <button on:click={handleFilterComplete}>Show Only completed</button>
  {#if todos.length ===0}
    <p>Loading Todos ...</p>
  {/if}
  <ul>
   {#each todos as todo}
     <Todo todo={todo} on:remove={handleRemove}/>
   {/each}
  </ul>
  
</main>