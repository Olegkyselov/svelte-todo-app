<script>
  import { Button, Col, Row, Input } from "sveltestrap";

  export let todo;
  export let deleteTodo;
  export let editTodo;

  let isEdit = false;
  let title = todo.title || "";
  let desc = todo.desc || "";

  function onUpdate() {
    editTodo(todo.id, { title, desc });
    isEdit = false;
  }
</script>

{#if isEdit}
  <div class="container">
    <div>
      <Row class="m-1">
        <Input bind:value={title} />
      </Row>
      <Row class="m-1">
        <Input type="textarea" bind:value={desc} />
      </Row>
    </div>
    <span>
      <Button color="success" on:click={onUpdate}>Update</Button>
    </span>
  </div>
{:else}
  <div class="container">
    <div class="section1">
      <p>{todo.title}</p>
      <p>{todo.desc}</p>
    </div>

    <span class="section2">
      <Button color="warning" outline on:click={() => deleteTodo(todo.id)}
        >Delete</Button
      >
      <Button color="info" outline on:click={() => (isEdit = true)}>Edit</Button
      >
    </span>
  </div>
{/if}

<style>
  .container {
    display: flex;
    width: 70%;
    justify-content: space-between;
    border: 2px solid #f5f5f5;
    padding: 1em;
    margin: 5px;
    border-radius: 5px;
  }
</style>
