<template>
  <main>
    <Form @item-added="addItem" />
    <ul>
      <li v-for="item in items" :key="'item-' + nanoid()">
        <Item :item="item"/>
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
  if (itemName === '') return;

  items.value.push({ name: itemName, done: "false" });
};
</script>