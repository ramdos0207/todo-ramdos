<script setup lang="ts">
import { computed, ref } from 'vue'

interface Item {
  name: string
  isCompleted: boolean
}

const items = ref<Item[]>([
  { name: 'todoリストの実装方針を決める', isCompleted: true },
  { name: 'vueを理解する', isCompleted: false }
])

const completedItems = computed(() => items.value.filter((task) => task.isCompleted))
const uncompletedItems = computed(() => items.value.filter((task) => !task.isCompleted))

const newItemName = ref('')

const addItem = () => {
  items.value.push({ name: newItemName.value, isCompleted: false })
  newItemName.value = ''
}
</script>

<template>
  <div>
    <div>todoList</div>
    <p>完了</p>
    <ul>
      <li v-for="item in completedItems" :key="item.name">
        <div v-if="item.isCompleted">名前: {{ item.name }}</div>
      </li>
    </ul>
    <p>未完了</p>
    <ul>
      <li v-for="item in uncompletedItems" :key="item.name">
        <button v-if="!item.isCompleted" @click="item.isCompleted=true" class="completeButton">完了</button>
        <p v-if="!item.isCompleted" class="itemName">名前: {{ item.name }}</p>
      </li>
    </ul>
    <br>
    <div>
      <label>
        名前
        <input v-model="newItemName" type="text" />
      </label>
      
      <button @click="addItem">追加</button>
    </div>
  </div>
</template>

<style>
.itemName{
    float:left;
}
.completeButton{
    float:left;
}
</style>