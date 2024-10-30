<template>
    <form @submit.prevent="handleSubmit">
        <input type="text" v-model="newItem" />
        <input type="submit" value="Добавить" />
    </form>

</template>

<script setup>
import { ref } from 'vue';

const newItem = ref('');

const emits = defineEmits(['item-added']);
const handleSubmit = () => {
    emits('item-added', newItem.value.trim());
    newItem.value = '';
};


</script>

<style scoped>

form {
    width: 70%;
}

input[type="text"] {
  display: block;
  border-radius: 5px;
  border: none;
  height: 1.2rem;
  width: 70%;
  margin: auto;
  margin-bottom: 10px;
}

input[type="text"]:focus {
  outline: 2px solid orange;
}

</style>