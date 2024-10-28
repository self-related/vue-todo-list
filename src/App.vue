<template>
  <div id="to-do-list">
    <h1>Лист</h1>
    <Form @item-added="addItem" />
    <button id="delete-all" @click="deleteAll">Удалить все</button>
    <ul>
      <li v-for="item in items" :key="'item-' + nanoid()" >
        <Item :item="item" @item-deleted="deleteItem" @item-status-changed="changeStatus"/>
      </li>
    </ul>
  </div>
</template>

<script setup>
import Form from './components/Form.vue';
import Item from './components/Item.vue';
import { ref } from 'vue';
import { nanoid } from 'nanoid';

const items = ref([]);

const addItem = (itemName) => {
  if (itemName === '') 
    return;
  if ( items.value?.find(item => item.name === itemName) ) {
    alert("Уже есть такой пункт!");
    return;
  }

  items.value.push({ name: itemName, done: false });
};

const deleteItem = (name) => {
  items.value = items.value.filter(item => item.name !== name);
  console.log(items.value);
};

const changeStatus = (name, status) => {
  items.value.find(item => item.name === name).done = status;
  console.log(items.value);

};

const deleteAll = () => {
  if (confirm("Удалить все элементы?")) {
    items.value = [];
  }
};
</script>

<style>
#to-do-list {
  background-color: #404040;
  border-radius: 15px;
  min-height: 500px;
  min-width: 300px;
  width: 50%;
  margin: auto;
  margin-top: 10vh;
  display: flex;
  flex-direction: column;
  justify-content: start;
  align-items: center;
}
#delete-all {
  background: none;
  border: none;
  margin: 5px;
  color: red;
  text-decoration: underline;
  cursor: pointer;
}
#delete-all:hover {
  color: blueviolet;
}

ul {
  width: 55%;
  display: flex;
  flex-direction: column;
  align-items: start;
}
li {
  list-style: none;
  max-width: 100%;
}
</style>