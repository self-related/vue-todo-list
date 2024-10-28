<template>
  <main>
    <Form @item-added="addItem" />
    <ul>
      <li v-for="item in items" :key="'item-' + nanoid()" >
        <Item :item="item" @item-deleted="deleteItem" @item-status-changed="changeStatus"/>
      </li>
    </ul>
  </main>
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
  if ( items.value.find(item => item.name === itemName) ) {
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
</script>