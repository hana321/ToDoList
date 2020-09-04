<template>
  <div class="item" v-bind:class="{ done: item.isChecked }">
      <label>
        <!-- <input type="checkbox" v-model="item.isChecked"> -->
        <li class="list-item">
          <template>
            <!-- isCheckedだったら -->
            <template v-if="item.isChecked">
              <i class="fa fa-check-circle icon-check icon" aria-hidden="true" @click="$emit('toggleClick')"></i>
            </template>
            <!-- !isCheckedだったら -->
            <template v-else>
              <i class="fa fa-circle-thin icon-check icon" aria-hidden="true" @click="$emit('toggleClick')"></i>
            </template>
          </template>
        </li>

        <template>
          <!-- 編集モードじゃなかったら -->
          <template v-if="item.editMode">
            <input type="text" v-model="item.title" class="editText" @keyup.enter="$emit('toggleEdit')">
          </template>
          <!-- 編集モードだったら -->
          <template v-else>
            <span @click="$emit('toggleEdit')" class="editText">{{item.title}}</span>
          </template>
        </template>

        <i @click="$emit('removeItem', item)" class="fa fa-trash icon-trash btn" aria-hidden="true"></i>
      </label>
  </div>
</template>

<script>
export default {
  name: "ToDo",
  props: ["item"],
};
</script>

<style>
  .item {
    overflow: hidden;
    padding: 15px 15px;
    background: #fff;
    border-bottom: 1px solid #e8e8e8;
    transition: .5s transform;
  }

  .done, .done .editText{
  background: #e5e5e5;
  color: #888;
}

  .label, .editText {
    font-size: 15px;
    border: none;
  }

.list-item {
  display: inline-block;
  line-height: 40px;
}

.icon {
  margin-right:15px;
}

.icon-check{
  font-size: 25px !important;
  color: rgba(89, 158, 175, 0.29);
  vertical-align: middle;
}

.icon-square, .icon-check, .icon-sort, .icon-trash{
  cursor: pointer;
  transition: .5s transform;
}

.icon-square:hover, .icon-check:hover, .icon-sort:hover, .icon-trash:hover{
  transform: scale(1.2);
  transition: .5s transform;
}
</style>