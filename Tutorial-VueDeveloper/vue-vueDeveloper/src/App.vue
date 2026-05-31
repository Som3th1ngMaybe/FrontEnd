<script setup>

import { ref, onMounted } from 'vue'
import CrudComponent from './components/CrudComponent.vue'
import api from './services/api'

const cruds = ref([])

async function readCruds() {

  const response = await api.get('/cruds')

  cruds.value = response.data
}

async function createCrud() {

  const colors = ['red', 'green']

  const newCrud = {
    name: Math.random()
      .toString(36)
      .substring(2, 10),

    color: colors[
      Math.floor(Math.random() * 2)
    ]
  }

  const response =
    await api.post('/cruds', newCrud)

  cruds.value.push(response.data)
}

async function updateCrud(id, color) {

  await api.patch(`/cruds/${id}`, {
    color
  })

  const crud =
    cruds.value.find(c => c.id === id)

  crud.color = color
}

async function deleteCrud(id) {

  await api.delete(`/cruds/${id}`)

  cruds.value =
    cruds.value.filter(
      crud => crud.id !== id
    )
}

onMounted(() => {
  readCruds()
})

</script>

<template>

  <h1>CRUD Demo</h1>

  <CrudComponent
    v-for="crud in cruds"
    :key="crud.id"
    v-bind="crud"
    @update="updateCrud"
    @delete="deleteCrud"
  />

  <button @click="createCrud">
    Add
  </button>

</template>
