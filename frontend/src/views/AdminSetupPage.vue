<template>
  <v-container>
    <v-content>
  <div class="ma-16" align="center">
    <h1>Sign up</h1>
    <br>
    <br>
    <br>
    <admin-setup-form @submit="onSubmit"/>
  </div>
   </v-content>
    </v-container>
</template>

<script>
import axios from 'axios'
import AdminSetupForm from '@/components/AdminSetupForm.vue'

export default {
  name: 'AdminSetupPage',
  components: {
    AdminSetupForm
  },
  methods: {
    onSubmit (payload) {
      console.log('payload: ' + payload.userId +
                  ', ' + payload.userName +
                  ', ' + payload.userPw)
      const { userId, userName, userPw } = payload
      axios.post('http://localhost:7777/users/setup',
        { userId, userName, userPw })
        .then(res => {
          alert('Register Success')
          this.$router.push({
            name: 'Home'
          })
        })
        .catch(err => {
          alert(err.response.data)
        })
    }
  }
}
</script>
