<template>
    <div class="container">
        <form class="form" @submit.prevent="handleRegister">
            <h3 class="text-center text-info">Sign Up</h3>
            <div class="form-group">
                <input type="text" v-model="name" placeholder="Enter name" class="form-control">
            </div>
            <div class="form-group">
                <input type="email" v-model="email" placeholder="Enter email" class="form-control">
            </div>
            <div class="form-group">
                <input type="password" v-model="password" placeholder="Enter password" class="form-control">
            </div>
            <div class="form-group">
                <input type="password" v-model="password_confirmation" placeholder="Enter confirm password" class="form-control">
            </div>
            <div class="form-group">
                <input type="submit" name="submit" class="btn btn-info btn-md font-weight-bold" value="Sign In">
            </div>
            <div id="register-link" class="text-right">
                Already have an account ? <router-link :to="{name: 'Login'}" class="text-info">Login here</router-link>
            </div>
        </form>
    </div>
</template>

<script>
import axios from "axios"

export default {
    name: "Register",
    data() {
        return {
            name: '',
            email: '',
            password: '',
            password_confirmation: ''
        }
    },
    methods: {
        async handleRegister()
        {
            if (this.name == '' || this.email == '' || this.password == '' || this.password_confirmation == '') {
                alert("Please enter all the needed fields.")
                return
            }

            if (this.password_confirmation !== this.password) {
                alert("Confirm password doesn't match with actual password.")
                return
            }

            const newUser = {
                name: this.name,
                email: this.email,
                password: this.password,
                password_confirmation: this.password_confirmation
            }

            await axios.post("http://127.0.0.1:8000/api/register", newUser, {
                headers: {
                // remove all the headers
                }
            }).then((res) => {
                if (res.status === 201) {
                    this.name = ''
                    this.email = ''
                    this.password = ''
                    this.password_confirmation = ''

                    this.$router.push('/login')
                }
            }).catch((err) => {
                console.log(err.response)
            })
        }
    }
}
</script>