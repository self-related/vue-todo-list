<template>
    <div>
        {{ item.name }}
        <button @click="handleClick">X</button>
    </div>
</template>

<script setup>
import { ref } from 'vue';
    const props = defineProps(["item"]);
    const item = ref(props.item);
    const emit = defineEmits(["item-deleted"]);

    const handleClick = () => {
        emit('item-deleted', item.value.name);
    };
</script>