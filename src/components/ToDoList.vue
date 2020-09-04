<template>
  <div class="container">
    <h1>My tasks</h1>
    <ToDoCreate @addToDo="addToDo"></ToDoCreate>

    <Search @searchItemChanged="searchItemChanged"></Search>

    <div class="lists">
      <ToDo v-for="item in filteredList" v-bind:item="item" v-bind:key="item.id" @removeItem="removeItem" @toggleClick="item.isChecked=!item.isChecked" @toggleEdit="item.editMode = !item.editMode"></ToDo>
    </div>
    <!-- <i @removeItem="removeItem" class="fa fa-trash icon-trash btn" aria-hidden="true"></i> -->
  </div>
</template>

<script>
import ToDoCreate from "./ToDoCreate.vue";
import Search from "./Search.vue";
import ToDo from "./ToDo.vue";

export default {
  name: "ToDoList",
  props: ["lists", "newItemTitle", "keyword"],
  components: {
    ToDo,
    ToDoCreate,
    Search,
  },

  methods: {
    // ToDoの追加
     addToDo: function(newItemTitle){
       if(newItemTitle){
         this.lists.push({
           title: newItemTitle,
           isChecked: false,
           editMode: false
        });
      }
      newItemTitle = '';
      this.saveToDo();
    },

    // deleteToDo: function(){
    //   this.lists = this.lists.filter(function(item){
    //     return item.isChecked === false;
    //   });
    //   this.saveToDo();
    // },

    removeItem: function(item){
      this.$emit('remove-todo', item);
      this.saveToDo();
    },


    // localStorageに保存するのはlocalStorage.setItem('フィールド名': 値)で簡単に実装できる。ただし配列のまま入れることができないので、文字列に変換するためJSON.stringifyで変換する。
    saveToDo: function(){
      localStorage.setItem('lists', JSON.stringify(this.lists));
    },

    // dataオプション内の配列itemsにブラウザ内のデータを持ってくるだけ。ブラウザ内のデータは単なる文字列なので、JSON.parseで配列に整える。ブラウザにデータがない時は空の配列となるように[]を入れ込む。
    loadTodo: function(){
      this.items = JSON.parse(localStorage.getItem('items'));
      if(!this.items){
        this.items = [];
      }
    },
  
    searchItemChanged : function(keyword){
      this.keyword = keyword;
      },

  },

  mounted: function(){
    this.loadTodo();
  },

  computed: {
    filteredList: function(){
      // 絞り込み後の商品リストを返す算出プロパティ
      var newList = this.lists;
      var filterWord = this.keyword && this.keyword.toLowerCase();

      if(filterWord){
        newList = newList.filter(function(row){
          return Object.keys(row).some(function(key){
            return String(row[key]).toLowerCase().indexOf(filterWord) > -1
          })
        })
      }
      return newList;
   }
  }
};

</script>

<style>

.container {
  width: 400px;
  margin: 100px auto;
}

 h1 {
   color:white
 }

 .lists{
    list-style: none;
    padding: 0;
    margin: 0;
    box-shadow: 0 2px 4px 0 rgba(0, 0, 0, 0.2), 0 25px 50px 0 rgba(0, 0, 0, 0.1);
    background: white;
    text-align: left;
    margin-bottom: 20px;
 }

 .item:hover{
  transform: scale(1.02);
  transition: .5s transform;
}

 /* .item {
     overflow: hidden;
  padding: 15px 15px;
  background: #fff;
  border-bottom: 1px solid #e8e8e8;
  transition: .5s transform;
 } */

 .btn {
   font-size: 20px;
   border: none;
   border-radius: 20px;
   float: right;
   background: #fef8e9;
   padding: 10px;
   color: pink;
 }
</style>
