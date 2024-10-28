<template>
    <div>
        {{ item.name }}
    </div>
</template>

<script setup>
import { ref } from 'vue';
    const props = defineProps(["item"]);
    const item = ref(props.item);
</script>