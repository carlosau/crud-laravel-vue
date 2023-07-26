<script setup>
import { ref } from 'vue';

const name = ref('Type name')

</script>

<template>
    <h2>{{ name }}</h2>
    <input type="text" v-model="name">
</template>
