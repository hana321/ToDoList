<template>
  <div class="searchBox">
    <i class="fa fa-search searchBox__icon"></i>
    <input type="text" v-on:keyup="$emit('searchItemChanged', keyword)" placeholder="検索してみてね" v-model="keyword" class="searchText">
  </div>
</template>

<script>
export default {
  name: "Search",
  // props: ['keyword']
}
</script>

<style>
.searchText {
  width: 100%;
  border: none;
  box-sizing: border-box;
  padding: 5px 10px;
  font-size: 16px;
  }

  .fa {
    display: inline-block;
    font: normal normal normal 14px/1 FontAwesome;
    font-size: inherit;
    text-rendering: auto;
    -webkit-font-smoothing: antialiased;
  }

  .searchBox__icon{
  width: 16px;
  font-size: 18px;
  margin-right: 5px;
  color: #888;
  z-index: 100;
}

.searchBox{
  width: 100%;
  height: 40px;
  border: 1px solid #e8e8e8;
  border-radius: 20px;
  margin-bottom: 15px;
  background: #fff;
  display: flex;
  align-items: center;
  padding: 0 10px;
  box-sizing: border-box;
}

</style>
