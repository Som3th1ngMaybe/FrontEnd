<script setup>

const props = defineProps({
id: Number,
name: String,
color: String
})

const emit = defineEmits([
'update',
'delete'
])

function updateColor(event) {
emit('update', props.id, event.target.value)
}

function deleteCrud() {
emit('delete', props.id)
}

function properCase(text) {
return text.charAt(0).toUpperCase() + text.slice(1)
}

</script>

<template>
    <div class="crud">
        <h3>{{ properCase(name) }}</h3>
        <select :value="color" @change="updateColor">
            <option value="red">Red</option>
            <option value="green">Green</option>
        </select>
        <button @click="deleteCrud">Delete</button>
    </div>
</template>