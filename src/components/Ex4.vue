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
    placeholder="Add an item"
    @keyup.enter="addItem"
  />
  <button type="button" @click="addItem">Add!</button>
</template>