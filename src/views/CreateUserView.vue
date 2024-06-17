<template>
  <div>
    <h1>Создание пользователя</h1>
    <form @submit.prevent="submitForm">
      <input v-model="user.name" type="text" placeholder="Имя" required>
      <input v-model="user.email" type="email" placeholder="Email" required>
      <input v-model="user.phone" type="tel" placeholder="Телефон" required>
      <input v-model="user.address" type="text" placeholder="Адрес" required>
      <button type="submit">Создать</button>
    </form>
  </div>
</template>

<script lang="ts">
import axios from '@/axios'
import { defineComponent } from 'vue'
import { User } from '@/types'

export default defineComponent({
  data (): { user: User } {
    return {
      user: {
        name: '',
        email: '',
        phone: '',
        address: ''
      }
    }
  },
  methods: {
    async submitForm () {
      try {
        const response = await axios.post('/users', this.user)
        alert('Пользователь создан: ' + response.data.id)
      } catch (error) {
        alert('Ошибка при создании пользователя: ' + error.message)
      }
    }
  }
})
</script>
