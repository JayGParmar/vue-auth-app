<template>
  <div id="app">
    <Nav />
    <router-view />
  </div>
</template>

<script>
import axios from "axios"
import Nav from "./components/Nav.vue"

export default {
  name: "App",
  // data() {
  //   return {
  //     user: null
  //   }
  // },
  components: {
    Nav
  },
  async created() {
    try {
      const res = await axios.get("http://127.0.0.1:8000/api/user", {
        headers: {
          "Authorization":"Bearer "+localStorage.getItem('token')
        }
      })

      if (res.status === 200) {
        this.$store.dispatch('user', res.data)

        // this.user = res.data
      }
    } catch (err) {
      console.log(err)
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>
