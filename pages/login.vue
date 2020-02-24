<template>
  <div class="login">
    <h1>Login Vuewewewe</h1>
    <form @submit.prevent="pressed">
      <div class="login">
        <input v-model="email" type="text" placeholder="email" />
      </div>
      <div class="password">
        <input v-model="password" type="password" placeholder="password" />
      </div>
      <button>Login</button>
    </form>
    <div v-if="error" class="error">{{ error.message }}</div>
  </div>
</template>

<script>
import * as firebase from 'firebase/app'
import 'firebase/auth'

export default {
  data() {
    return {
      email: '',
      password: '',
      error: ''
    }
  },
  methods: {
    pressed() {
      firebase
        .auth()
        .signInWithEmailAndPassword(this.email, this.password)
        .then((data) => {
          console.log(data)
          this.$router.push('/secret')
        })
        .catch((error) => {
          this.error = error
          console.log(error)
        })
    }
  }
}
</script>

<style scoped>
.login {
  margin-top: 50px;
  display: flex;
  width: 100%;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}
form {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}

input {
  width: 400px;
  padding: 30px;
  margin: 20px;
  font-size: 21px;
}

button {
  width: 400px;
  height: 75px;
  font-size: 100%;
}

.error {
  color: red;
}
</style>
