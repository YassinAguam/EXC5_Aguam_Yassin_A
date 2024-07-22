<template>
 <div>
    <h1>Attendance Monitoring Application</h1>
    <AttendanceForm @add-attendance="addAttendance" />
    <AttendanceList :attendanceData="attendanceData" />
  </div>
</template>

<script setup>
import { ref } from 'vue'
import AttendanceForm from '../components/AttendanceForm.vue'
import AttendanceList from '../components/AttendanceList.vue'

const attendanceData = ref([])

const addAttendance = (attendance) => {
  attendanceData.value.push(attendance)
}
</script>
