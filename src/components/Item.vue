<template>
    <div :class="isDone ? 'done item' : 'item'">
        <input type="checkbox" v-model="isDone" @change="handleCheck">
        <p>{{ item.name }}</p>
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
.item {
    display: flex;
    gap: 1rem;
    max-width: 100%;

}
p {
    max-width: 100%;
    word-wrap: break-word;
}
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