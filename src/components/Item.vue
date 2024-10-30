<template>
    <div class="item">
        <input type="checkbox" v-model="isDone" @change="handleCheck">
        <p :class="isDone ? 'done' : ''">{{ item.name }}</p>
        <a href="javascript:void(0)" @click="handleClick" :class="isDone ? 'done' : ''">удалить</a>
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
    background-color: #505050;
    margin-top: 1rem;
    border-radius: 10px;
    padding: 1rem;

}
p {
    max-width: 100%;
    word-wrap: break-word;
}
.done {
    color: gray;
    text-decoration: line-through;
}


a {
    color: #f03a3a;
    vertical-align: super;
    font-size: 0.7rem;
}

a.done {
    color: rgb(233, 82, 82);
    text-decoration: underline;
}

a:hover {
    color: blueviolet;
}

input[type="checkbox"] {
    accent-color: orange;
}
</style>