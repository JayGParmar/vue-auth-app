<template>
    <div id="nav">
        <div id="navbar" class="navbar navbar-expand navbar-fixed-top">
            <div class="container">
                <div class="navbar-brand">
                    <router-link :to="{name: 'Home'}">Vue Application</router-link>
                </div>
                <ul class="nav" v-if="!user">
                    <li class="nav-item">
                        <router-link :to="{name: 'Login'}" class="nav-link">Login</router-link>
                    </li>
                    <li class="nav-item">
                        <router-link :to="{name: 'Register'}" class="nav-link">Register</router-link>
                    </li>
                </ul>
                <ul class="nav" v-else>
                    <li class="nav-item">
                        <span class="nav-link font-weight-bold logout" @click="handleLogout">Logout</span>
                    </li>
                </ul>
            </div>
        </div>
    </div>
</template>

<script>
import axios from "axios"
import { mapGetters } from "vuex"

export default {
    name: "Nav",
    // props: {
    //     user: Object
    // },
    methods: {
        async handleLogout() {
            if (confirm("Are you sure you want to logout ?")) {
                await axios.post("http://127.0.0.1:8000/api/logout", {id: this.user.id}, {
                    headers: {
                        "Authorization":"Bearer "+localStorage.getItem('token')
                    }
                }).then((res) => {
                    if (res.status === 200) {
                        localStorage.removeItem('token')
                        this.$store.dispatch('user', null)
                        this.$router.push('/login')
                    }
                }).catch((err) => {
                    console.log(err)
                })
            }
        }
    },
    computed: {
        ...mapGetters(['user'])
    }
}
</script>

<style scoped>
.logout {
    cursor: pointer;
}
</style>