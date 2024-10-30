<template>
  <div id="to-do-list">
    <h1>Лист</h1>
    <Form @item-added="addItem" />
    <a href="javascript:void(0)" id="delete-all" @click="deleteAll">Удалить все</a>
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
  font-size: 0.8rem;
  background: none;
  border: none;
  margin: 5px;
  color: #f03a3a;
  text-decoration: underline;
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

a, p {
  text-shadow: 0.03rem 0.03rem 1px black !important;

}

input[type="submit"], button {
  display: block;
  margin: auto;
  background-color: orange;
  border: none;
  border-radius: 5px;
  padding: 5px;
  color: white;
  font-weight: bold;
  text-shadow: 0.05rem 0.05rem 0.05rem black;
  cursor: pointer;
}

input[type="submit"]:hover, button:hover {
    background-color: blueviolet;
}

input[type="submit"]:active, button:active {
    background-color: #f03a3a;
}

input[type="text"] {
  border-radius: 5px;
  border: none;
  margin: auto;
}

input[type="text"]:focus {
  outline: 2px solid orange;
}

</style>