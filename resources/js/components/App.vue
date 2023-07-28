<script setup>
import { ref } from 'vue';

const header = ref('Crud App Vue JS')
const items = ref([
    {id: 1, label: "Learn Laravel", accomplishedSkill: false},
    {id: 2, label: "Build Laravel App", accomplishedSkill: false},
    {id: 3, label: "Earn money with Laravel", accomplishedSkill: false}
])
const newItem = ref('')
const editing = ref(false)
const isHighPriority = ref(false)
const addNewItem = () => {
    items.value.push({id: items.value.length + 1, label: newItem.value})
    newItem.value = ''
}
const editSkill = (editvalue) => {
    editing.value = editvalue
}
const clearAll = () => {
    items.value = ([])
}
const accomplishedFn = (item) => {
    item.accomplishedSkill = true
}
const accomplishedFnUndo = (item) => {
    item.accomplishedSkill = false
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
        <button @click="clearAll()">
            Clear All
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
        <li
        v-for="item in items"
        :key="item.id"
        :class="{strikeout: item.accomplishedSkill}"
        >
        {{ item.label }}
        <button
        @click="accomplishedFn(item)"
        >
        Ok
        </button>
        <button
        v-if="item.accomplishedSkill"
        @click="accomplishedFnUndo(item)"
        >
        Undo
        </button>
        </li>
    </ul>

    <p v-if="!items.length">
        No skills added
    </p>
</template>
