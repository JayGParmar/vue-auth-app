<template>
    <div class="home">
      <div v-if="user">
        <h1>{{ "Welcome "+user.name }}</h1>
        <h3>
          <u>Login user details</u>
        </h3>
        <p>Name : {{ user.name }}</p>
        <p>Email : {{ user.email }}</p>
        <p>Started On : {{ user.created_at }}</p>
      </div>
      <div v-else>
        <h3>Unauthenticated !!</h3>
      </div>
    </div>
</template>

<script>
import {mapGetters} from "vuex"

export default {
  name: 'Home',
  computed: {
      ...mapGetters(['user'])
  }
}
</script>

<style scoped>
.no-user h1 {
  margin: 0 auto;
  background: #eeeeee;
  padding: 20px;
  width: 40%;
}
.no-user h3 {
  margin: 0 auto;
  margin-top: 2%;
  background: #eeeeee;
  padding: 15px;
  width: 30%;
}
.no-user p {
  margin: 0 auto;
  margin-top: 2%;
  background: #eeeeee;
  padding: 10px;
  width: 20%;
}
</style>