<script setup>
import { ref } from 'vue'

const items = ref(['keyboard', 'mouse', 'iPhone', 'macbook', 'adapter'])
const newItem = ref('')

function del(index) {
  items.value.splice(index, 1)
}

function addItem() {
  const text = newItem.value.trim()
  if (text !== '') {
    items.value.push(text)
    newItem.value = ''
  }
}

function handleKeyDown(event) {
  // Checks both keyCode and key name, and prevents triggering during IME input
  if ((event.key === 'Enter' || event.keyCode === 13) && !event.isComposing) {
    event.preventDefault()
    addItem()
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

  <input 
    type="text" 
    v-model="newItem" 
    @keydown="handleKeyDown" 
  />
  <button type="button" @click="addItem">Add!</button>
</template>