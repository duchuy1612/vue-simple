<script setup lang="ts">
import { ref } from 'vue'
import DashboardLayout from '../components/DashboardLayout.vue'

interface User {
  name: string
  email: string
  title: string
  title2: string
  status: string
  role: string
}

const testUser: User = {
  name: 'John Doe',
  email: 'john@example.com',
  title: 'Software Engineer',
  title2: 'Web dev',
  status: 'Active',
  role: 'Owner',
}

const users = ref<User[]>([...Array(10).keys()].map(() => testUser))
</script>

<template>
  <div>
    <DashboardLayout />
    <h3 class="text-3xl font-medium text-gray-700">
      Dashboard
    </h3>
  </div>
</template>
