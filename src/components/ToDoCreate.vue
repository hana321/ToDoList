<template>
  <div>
    <input type="text" placeholder="ToDoを入力をする" v-model="newItemTitle" @keyup.enter="$emit('addToDo', newItemTitle)" class="createTodo">
  </div>
</template>

<script>
  export default {
    name: "ToDoCreate",
    props: ['newItemTitle', 'item']
  };
</script>

<style>
.createTodo {
  padding: 5px 10px;
  height: 40px;
  font-size: 16px;
  width: 100%;
  box-sizing: border-box;
  border: 1px solid #e8e8e8;
  margin-bottom: 30px;
  }
</style>
