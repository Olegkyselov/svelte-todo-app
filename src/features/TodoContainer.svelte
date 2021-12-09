<script>
  import { onMount } from "svelte";
  import TodoItem from "../components/TodoItem.svelte";
  import TodoInput from "../components/TodoInput.svelte";

  const BASE_URL = "https://61b252e4c8d4640017aaf36b.mockapi.io";

  function apiCall(url, method, body) {
    return fetch(url, {
      headers: {
        "Content-Type": "application/json",
      },
      method: method || "GET",
      body: body ? JSON.stringify(body) : undefined,
    });
  }

  let data = [];

  onMount(async () => {
    const res = await apiCall(`${BASE_URL}/todos`);
    data = await res.json();
  });

  async function addTodo(todo) {
    console.log(todo);
    try {
      const res = await apiCall(`${BASE_URL}/todos`, "post", todo);
      const newTodo = await res.json();
      console.log(newTodo);
      data = [...data, newTodo];
    } catch (err) {
      console.log(err.message);
    }
  }

  async function deleteTodo(id) {
    try {
      const res = await apiCall(`${BASE_URL}/todos/${id}`, "DELETE");

      if (res.ok) {
        const deletedTodo = await res.json();
        console.log(deletedTodo);
        data = data.filter((x) => x.id !== id);
      } else {
        console.log(res);
      }
    } catch (err) {
      console.log(err.message);
    }
  }

  async function editTodo(id, todo) {
    try {
      const res = await apiCall(`${BASE_URL}/todos/${id}`, "PUT", todo);
      const updated = await res.json();
      data = data.map((item) => {
        if (item.id === id) {
          return updated;
        }
        return item;
      });
    } catch (err) {
      console.log(err.message);
    }
  }
</script>

<section>
  <TodoInput {addTodo} />

  <h2 class="m-4">Todo List</h2>
  {#each data as todo (todo.id)}
    <TodoItem {todo} {deleteTodo} {editTodo} />
  {/each}
</section>

<style>
  section {
    padding: 1em;
    width: 70%;
    margin: 0 auto;
  }

  @media (min-width: 640px) {
    section {
      max-width: none;
    }
  }
</style>
