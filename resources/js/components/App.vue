<script setup>
import { ref , computed } from 'vue';

const header = ref('Crud App Vue JS')
const items = ref([
    {id: 1, label: "Learn Laravel", accomplishedSkill: false, isHighPriority: false},
    {id: 2, label: "Build Laravel App", accomplishedSkill: false, isHighPriority: false},
    {id: 3, label: "Earn money with Laravel", accomplishedSkill: false, isHighPriority: false}
])
const isHighPriority = ref(false)
const characterCount = computed(() => {
    return newItem.value.length
})
const maxAllowedChar = 20
const newItem = ref('')
const editing = ref(false)
const addNewItem = () => {
    items.value.push({
        id: items.value.length + 1,
        label: newItem.value,
        isHighPriority: isHighPriority.value
    })
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
        v-bind:disabled="newItem.length > maxAllowedChar"
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
    <p v-if="editing" class="counter">
        {{ characterCount }}/20
    </p>
    <ul style="list-style: none;">
        <li
        v-for="item in items"
        :key="item.id"
        :class="{strikeout: item.accomplishedSkill, priority: item.isHighPriority}"
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
