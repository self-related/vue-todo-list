<template>
    <div :class="isDone ? 'done asd' : ''">
        <input type="checkbox" v-model="isDone" @change="handleCheck">
        {{ item.name }}
        <button @click="handleClick" :class="isDone ? 'done' : ''">X</button>
    </div>
</template>

<script setup>
import { ref } from 'vue';
    const props = defineProps(["item"]);
    const emit = defineEmits(["item-deleted", "item-status-changed"]);
    
    const item = ref(props.item);
    const isDone = ref(props.item.done);

    const handleClick = () => {
        emit('item-deleted', item.value.name);
    };
    const handleCheck = () => {
        emit("item-status-changed", item.value.name, isDone.value);
    };
</script>

<style scoped>

div[class~=done] {
    color: gray;
    text-decoration: line-through;
}


button {
    background: none;
    color: red;

    border: none;
    vertical-align: super;
    cursor: pointer;
}

div[class~=done] button {
    color: rgb(233, 82, 82);
}
</style>