<template>
  <div v-if="user">
    <h1>{{ user.name }}</h1>
    <p>Email: {{ user.email }}</p>
    <p>Phone: {{ user.phone }}</p>
    <p>Address: {{ user.address.street }} {{ user.address.suite }} {{ user.address.city }} {{ user.address.zipcode }}</p>
    <p>Company: {{ user.company.name }} {{ user.company.catchPhrase }} {{ user.company.bs }}</p>
  </div>
  <div v-else>
    Загрузка данных пользователя...
  </div>
</template>

<script lang="ts">
import axios from '@/axios'
import { defineComponent } from 'vue'

export default defineComponent({
  data () {
    return {
      user: null
    }
  },
  async mounted () {
    const response = await axios.get(`/users/${this.$route.params.id}`)
    this.user = response.data
  }
})
</script>
