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
      {{ item }} <button @click="del(index)">Delete!</button>
    </li>
  </ul>

  <!-- Input and Add button placed below the list -->
  <input v-model="newItem" placeholder="" />
  <button @click="addItem">Add!</button>
</template>