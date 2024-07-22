<template>
  <div class="list-container">
    <a-table :columns="columns" :data-source="data">
      <template #name="{ text }">
        <a-tag color="blue">{{ text }}</a-tag>
      </template>
      <template #datetime="{ text }">
        <span>{{ text }}</span>
      </template>
    </a-table>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const columns = [
  { title: 'Name', dataIndex: 'name', key: 'name', slots: { customRender: 'name' } },
  { title: 'Date & Time', dataIndex: 'datetime', key: 'datetime', slots: { customRender: 'datetime' } },
]

const data = ref([])
</script>

<style scoped>
.list-container {
  background: white; 
  padding: 24px;
  border-radius: 8px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}
</style>
