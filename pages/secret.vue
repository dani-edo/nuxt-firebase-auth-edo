<template>
  <div>
    <h1>This is Secret Info</h1>
  </div>
</template>

<script>
import * as firebase from 'firebase/app'
import { getUserFromCookie } from '@/helpers'
import 'firebase/auth'

export default {
  asyncData({ req, redirect }) {
    if (process.server) {
      const user = getUserFromCookie(req)
      console.log(user)
      if (!user) {
        redirect('/login')
      }
    } else {
      const user = firebase.auth().currentUser
      console.log('client user: ', user)
      if (!user) {
        redirect('/login')
      }
    }
  }
}
</script>

<style lang="scss" scoped></style>
