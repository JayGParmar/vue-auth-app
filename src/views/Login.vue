<template>
    <div class="container">
        <form class="form" @submit.prevent="handleLogin">
            <h3 class="text-center text-info">Sign In</h3>
            <div class="form-group">
                <input type="email" v-model="email" placeholder="Enter email" class="form-control">
            </div>
            <div class="form-group">
                <input type="password" v-model="password" placeholder="Enter password" class="form-control">
            </div>
            <div class="form-group">
                <input type="submit" name="submit" class="btn btn-info btn-md font-weight-bold" value="Sign In">
            </div>
            <div id="register-link" class="text-right">
                Don't have an account ? <router-link :to="{name: 'Register'}" class="text-info">Register here</router-link>
            </div>
        </form>
    </div>
</template>

<script>
import axios from "axios"

export default {
    name: "Login",
    data() {
        return {
            email: '',
            password: ''
        }
    },
    methods: {
        async handleLogin() {

            if (this.email == '' || this.password == '') {
                alert("Please enter the credentials.")
                return
            }

            const parameters = {
                email: this.email,
                password: this.password
            }

            await axios.post("http://127.0.0.1:8000/api/login", parameters, {
                headers: {
                    // remove all the headers
                }
            }).then((res) => {
                if (res.status === 200) {
                    const result = res.data

                    localStorage.setItem('token', result.data.token)
                    this.$store.dispatch('user', result.data.user)
                    this.$router.push('/')
                }
            }).catch((err) => {
                console.log(err.response)
            })
        }
    }
}
</script>