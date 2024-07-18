<script lang="ts" setup>
import { ref } from 'vue';
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome';
import { faEdit } from '@fortawesome/free-solid-svg-icons';
import { faRemove } from '@fortawesome/free-solid-svg-icons';

const arr = ref<any[]>([]);
const text = ref<string>("");

const onSubmit = (): void => {
  if(text.value === "") return;

  arr.value.push({
    title: text.value,
    done: false,
    id: 1,
  });
  text.value = "";
}

const removeItem = (id: number) => {
  console.log(id);
}

const editItem = (id: number) => {
  console.log(id);
}

const markDone = (id: number) => {
  console.log(id);
}

</script>

<template>
  <div class="avata">
    <img src="/assets/vue.svg" alt="avata">
  </div>

  <form class="form-list" @submit.prevent="onSubmit">
    <h2 class="label-wrapper">
      <label for="new-todo-input">
        What needs to be done?
      </label>
    </h2>
    <input 
      v-model="text" 
      name="todo" 
      id="new-todo-input">
    <button type="submit">Add</button>
  </form>

  <ul class="todo-list">
    <li class="todo-list-item" v-for="(item, index) in arr" :key="index">
      <span :style="{textDecoration: item.done ? 'line-through' : 'none'}">{{ item.title }}</span>
      <div class="icon">
        <input type="checkbox" @change="markDone(item.id)">
        <FontAwesomeIcon :icon="faEdit" class="icon-edit" @click="editItem(item.id)"/>
        <FontAwesomeIcon :icon="faRemove" class="icon-remove" @click="removeItem(item.id)"/>
      </div>      
    </li>    
  </ul>
</template>

<style scoped>
.avata {
  background: #fff;
  border-radius: 50%;
  width: 50px;
  height: 50px;
  margin-left: auto;
  margin-right: auto;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 3px;
}

.form-list {
  display: flex;
  flex-direction: column;
  gap: 10px;
}

.todo-list {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  margin-left: -30px;
  overflow-y: scroll;
  max-height: 180px;
}

.todo-list-item {
  text-align: left;
  font-size: medium;
  width: 100%;
  display: flex;
  justify-content: space-between;
  margin-bottom: 5px;
}

.icon {
  display: flex;
  gap: 10px;
  align-items: center;
}
</style>
