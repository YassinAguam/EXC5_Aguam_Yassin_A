<template>
  <Layout>
    <div class="content">
      <h1 class="title">Attendance Monitoring Application</h1>
      <AttendanceForm @add-attendance="addAttendance" />
      <div class="attendance-list">
        <h2>Recorded Attendance</h2>
        <a-table :columns="columns" :data-source="attendanceData" :pagination="{ pageSize: 5 }">
          <template #name="{ text }">
            <a-tag color="blue">{{ text }}</a-tag>
          </template>
          <template #datetime="{ text }">
            <span>{{ text }}</span>
          </template>
        </a-table>
        <div class="summary">
          <p>Total Records: {{ attendanceData.length }}</p>
        </div>
      </div>
    </div>
  </Layout>
</template>

<script setup>
import { ref } from 'vue'
import Layout from '~/components/Layout.vue'
import AttendanceForm from '~/components/AttendanceForm.vue'

const attendanceData = ref([])

const columns = [
  { title: 'Name', dataIndex: 'name', key: 'name', slots: { customRender: 'name' } },
  { title: 'Date & Time', dataIndex: 'datetime', key: 'datetime', slots: { customRender: 'datetime' } },
]

const addAttendance = (attendance) => {
  attendanceData.value.push(attendance)
}
</script>

<style scoped>
.content {
  background: #f3f4f6; 
  padding: 24px;
  border-radius: 8px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}

.title {
  font-size: 32px;
  font-weight: bold;
  margin-bottom: 20px;
}

.attendance-list {
  margin-top: 20px;
}

.attendance-list h2 {
  margin-bottom: 10px;
}

.summary {
  margin-top: 20px;
}
</style>
