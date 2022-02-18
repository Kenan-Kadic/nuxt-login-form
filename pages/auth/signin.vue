<template>
<v-app>
        <v-container fluid pa-0>
            <v-row align="center" justify="center"
                style="height:100vh" dense>
                    <v-card class="blue" max-width="600">
                      <v-card-title>EverBlue</v-card-title>
                    <v-card-text>
                      <v-form>
                        <v-text-field
                        label="Login"
                        name="login"
                        prepend-icon="mdi-account"
                        type="text"
                        v-model="auth.email"
                        >
                        </v-text-field>

                        <v-text-field
                        label="password"
                        name="password"
                        prepend-icon="mdi-lock"
                        type="password"
                        v-model="auth.password"
                        >
                        </v-text-field>
                      </v-form>
                    </v-card-text>
                    </v-card>
            </v-row>
        </v-container>
</v-app>
</template>

<script>
export default {
  layout: 'signin',
  data() {
    return {
      snackbar: false,
      snackbarText: 'No error message',
      auth: {
        email: '',
        password: ''
      }
    }
  },
  methods: {
    login() {
      let that = this
      this.$fire.auth.signInWithEmailAndPassword(this.auth.email, this.auth.password)
      .catch(function (error){
        that.snackbarText = error.message
        that.snackbar = true
      }).then((user) => {
        //we are signed in
        $nuxt.$router.push('/')
      })
    }
  }
}
</script>
