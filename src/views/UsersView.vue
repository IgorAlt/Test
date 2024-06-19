<template>
  <div>
    <h1>Список пользователей</h1>
    <ul class="userList">
      <li v-for="user in users" :key="user.id" class="userList_userItem">
        <router-link :to="'/user/' + user.id" class="userList_userItem_userLink">{{ user.name }}</router-link>
      </li>
    </ul>
  </div>
</template>

<script lang="ts" setup>
import { ref, onMounted } from 'vue'
import axios from '@/axios'
import { User } from '@/types'

const users = ref<User[]>([])

onMounted(async () => {
  const response = await axios.get('/users')
  users.value = response.data
})
</script>

<style lang="scss">
.userList {
  list-style: none;
  padding: 0;

  &_userItem {
    margin: 10px 0;

    &_userLink {
      text-decoration: none;
      color: #42b983;
    }
  }
}
</style>
