  <template>
    <div class="form-container">
      <a-form @submit="handleSubmit" layout="vertical">
        <a-form-item label="Name">
          <a-input v-model="form.name" placeholder="Enter your name" />
        </a-form-item>
        <a-form-item label="Date">
          <a-date-picker v-model="form.date" placeholder="Select date" />
        </a-form-item>
        <a-form-item label="Time">
          <a-time-picker v-model="form.time" placeholder="Select time" />
        </a-form-item>
        <a-form-item>
          <a-button type="primary" html-type="submit">Submit</a-button>
        </a-form-item>
      </a-form>

      <!-- Display the recorded attendance -->
      <div class="attendance-list">
        <h2>Recorded Attendance</h2>
        <a-table :columns="columns" :data-source="data">
          <template #name="{ text }">
            <a-tag color="blue">{{ text }}</a-tag>
          </template>
          <template #datetime="{ text }">
            <span>{{ text }}</span>
          </template>
        </a-table>
      </div>
    </div>
  </template>

  <script setup>
  import { ref } from 'vue'
  import { message } from 'ant-design-vue'

  const form = ref({
    name: '',
    date: null,
    time: null,
  })

  // Define emit
  const emit = defineEmits(['add-attendance'])

  const data = ref([])

  const columns = [
    { title: 'Name', dataIndex: 'name', key: 'name', slots: { customRender: 'name' } },
    { title: 'Date & Time', dataIndex: 'datetime', key: 'datetime', slots: { customRender: 'datetime' } },
  ]

  const handleSubmit = (e) => {
    e.preventDefault()
    if (form.value.name && form.value.date && form.value.time) {
      const newAttendance = {
        key: Date.now().toString(),
        name: form.value.name,
        datetime: `${form.value.date.format('YYYY-MM-DD')} ${form.value.time.format('HH:mm:ss')}`,
      }
      data.value.push(newAttendance)
      emit('add-attendance', newAttendance)
      form.value.name = ''
      form.value.date = null
      form.value.time = null

      message.success('Attendance added successfully!')
    }
  }
  </script>

  <style scoped>
  .form-container {
    background: lightblue; 
    padding: 24px;
    border-radius: 8px;
    box-shadow: 0 4px 6px black;
  }

  .attendance-list {
    margin-top: 20px;
  }

  .attendance-list h2 {
    margin-bottom: 10px;
  }
  </style>
