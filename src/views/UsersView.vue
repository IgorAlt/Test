<template>
  <div>
    <h1>Список пользователей</h1>
    <ul class="user-list">
      <li v-for="user in users" :key="user.id" class="user-item">
        <router-link :to="'/user/' + user.id" class="user-link">{{ user.name }}</router-link>
      </li>
    </ul>
  </div>
</template>

<script lang="ts">
import axios from '@/axios'
import { defineComponent } from 'vue'
import { User } from '@/types'

export default defineComponent({
  data (): { users: User[] } {
    return {
      users: []
    }
  },
  async mounted () {
    const response = await axios.get('/users')
    this.users = response.data
  }
})
</script>

<style lang="scss" scoped>
@import '@/styles/users.scss';
</style>
