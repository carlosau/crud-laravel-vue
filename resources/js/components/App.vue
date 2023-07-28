<script setup>
import { ref } from 'vue';

const header = ref('Crud App Vue JS')
const items = ref([
  /*   {id: 1, label: "Learn Laravel"},
    {id: 2, label: "Build Laravel App"},
    {id: 3, label: "Earn money with Laravel"} */
])
const newItem = ref('')
const editing = ref(false)
const isHighPriority = ref(false)
const addNewItem = () => {
    items.value.push({id: items.value.length + 1, label: newItem.value})
    newItem.value = ''
}
const editSkill = (evalue) => {
    editing.value = evalue
}
</script>

<template>
    <div>
        <h2>{{ header }}</h2>
        <button v-if="editing" @click="editSkill(false)">
            X
        </button>
        <button v-else @click="editSkill(true)">
            Create Skill
        </button>
    </div>
    <form
    class="add-item-form"
    v-if="editing"
    @submit.prevent="addNewItem"
    >
        <input
        type="text"
        v-model="newItem"
        placeholder="Add new Skill"
        >
        <button
        v-bind:disabled="newItem.length < 5"
        class="btn"
        type="submit"
        >
            Add skill
        </button>
        <label>
            <input type="checkbox"
            v-model="isHighPriority"
            >
            High Priority
        </label>
        ({{ isHighPriority }})
    </form>

    <ul style="list-style: none;">
        <li v-for="item in items" :key="item.id">{{ item.label }} </li>
    </ul>

    <p v-if="!items.length">
        No skills added
    </p>
</template>
