<script>
  import { Button, Row, Col, Input, Label } from "sveltestrap";

  export let addTodo;

  let title = "";
  let desc = "";

  function onAdd() {
    addTodo({ title, desc });
    title = "";
    desc = "";
  }
</script>

<div>
  <Row cols={2} class="m-2">
    <Col>
      <Label for="title">Title</Label>
      <Input bind:value={title} placeholder="Enter Todo title" />
    </Col>
  </Row>
  <Row cols={2} class="m-2">
    <Col>
      <Label for="desc">Description</Label>
      <Input
        type="textarea"
        bind:value={desc}
        name="desc"
        placeholder="Enter description"
      />
    </Col>
  </Row>
  <Row cols={2}>
    <Col>
      <span>
        <Button color="success" on:click={onAdd}>Add Todo</Button>
      </span>
    </Col>
  </Row>
</div>

<style>
    span {
        float: right;
    }
</style>