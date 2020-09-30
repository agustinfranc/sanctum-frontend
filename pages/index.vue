<template>
  <v-row justify="center" align="center">
    <v-col cols="12" sm="8" md="6">
      <v-card>
        <v-card-title class="headline">
          Welcome to the Vuetify + Nuxt.js template
        </v-card-title>
        <v-card-text>
          <p>
            Vuetify is a progressive Material Design component framework for
            Vue.js. It was designed to empower developers to create amazing
            applications.
          </p>
          <p>{{ user }}</p>
          <form @submit.prevent="login()">
            <input v-model="form.email" type="text" />
            <input v-model="form.password" type="text" />
            <button>login</button>
          </form>
        </v-card-text>
      </v-card>
    </v-col>
  </v-row>
</template>

<script>
import axios from 'axios'
axios.defaults.withCredentials = true
axios.defaults.baseURL = 'http://localhost:8000/';

export default {
  data: () => ({
    user: '',
    form: {
      email: '',
      password: '',
    },
  }),
  methods: {
    login() {
      axios.get('sanctum/csrf-cookie').then((response) => {
        // Login...
        axios.post('login', this.form).then((res) => {
          console.log(res)
        })
      })
    },
  },
}
</script>
