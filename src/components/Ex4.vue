<script setup>
import { ref } from 'vue'

const items = ref(['keyboard', 'mouse', 'iPhone', 'macbook', 'adapter'])
const newItem = ref('')

function del(index) {
  items.value.splice(index, 1)
}

function addItem() {
  if (newItem.value.trim() !== '') {
    items.value.push(newItem.value.trim())
    newItem.value = ''
  }
}
</script>

<template>
  <h2>Shopping Cart</h2>

  <ul>
    <li v-for="(item, index) in items" :key="index">
      {{ item }} <button type="button" @click="del(index)">Delete!</button>
    </li>
  </ul>

  <!-- Form handles Enter key and prevents page refresh -->
  <form @submit.prevent="addItem">
    <input v-model="newItem" />
    <button type="submit">Add!</button>
  </form>
</template>