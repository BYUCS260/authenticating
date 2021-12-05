<template>
<div>
  <Admin v-if="user && user.role === 'admin'" />
  <MyTickets v-else-if="user" />
  <HomePage v-else />
</div>
</template>

<script>
import HomePage from '@/components/HomePage.vue'
import MyTickets from '@/components/MyTickets.vue'
import Admin from '@/components/Admin.vue'
import axios from 'axios';
export default {
  name: 'home',
  components: {
    HomePage,
    MyTickets,
    Admin
  },
  async created() {
    try {
console.log("GET Users");
      let response = await axios.get('/api/users');
      this.$root.$data.user = response.data.user;
console.log(this.$root.$data.user);
console.log(response.data.user);
    } catch (error) {
console.log("Get User Error");
      this.$root.$data.user = null;
    }
  },
  computed: {
    user() {
console.log("computed user");
console.log(this.$root.$data.user);
      return this.$root.$data.user;
    }
  }
}
</script>

