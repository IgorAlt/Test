<template>
  <div>
    <h1>Список пользователей</h1>
    <ul :class="style['user-list']">
      <li v-for="user in users" :key="user.id" :class="style['user-item']">
        <router-link :to="'/user/' + user.id" :class="style['user-link']">{{ user.name }}</router-link>
      </li>
    </ul>
  </div>
</template>

<script lang="ts">
import axios from '@/axios'
import { defineComponent } from 'vue'
import { User } from '@/types'
import style from '@/styles/users.module.scss'

export default defineComponent({
  data (): { users: User[] } {
    return {
      users: []
    }
  },
  computed: {
    style () {
      return style
    }
  },
  async mounted () {
    const response = await axios.get('/users')
    this.users = response.data
  }
})
</script>
