<template>
  <div id="app">
    <ToDoList v-bind:lists="lists" @remove-todo="removeItem"></ToDoList>
  </div>
</template>

<script>
import ToDoList from "./components/ToDoList.vue";

export default {
  data: function () {
    return {
      lists: [
        {
          title: '掃除をする', isChecked: false, editMode: false
        },
        {
          title: 'ご飯をつくる', isChecked: false, editMode: false
        },
      ],
      newItemTitle: '',
      keyword: '',
    };
  },

  components: {
    ToDoList,
  },

  methods: {
    removeItem(item){
      this.lists = this.lists.filter((todo) => todo !== item);
    },
  }
};

</script>

<style>
  body {
    background: #80d8d0;
  }
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }


  

</style>
