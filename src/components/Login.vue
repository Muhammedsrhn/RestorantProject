<template>
    {{loginCheck()}}
    <img src="../assets/logo.png" />
    <h1>Login</h1>
    <div class="form">
        <input type="text" placeholder="Enter a Email" v-model="email">
        <input type="password" placeholder="Enter a Password" v-model="password">
        <button class="btn" v-on:click="login">Submit</button>
        <p class="login-error" id="loginErr">Invalid Email or Password</p>
        <router-link to="/sign-up">
            <p class="ı">I Have No Account</p>
        </router-link>
    </div>
</template>
<script>
import axios from 'axios';
export default {
    name: "Login",
    data() {
        return {
            email: '',
            password: '',
        }
    },

    methods: {
        goSignup() {
            this.$router.push({ name: "SignUp" });
        },
        async login() {
            let request = await axios.get(
                `http://localhost:3000/user?email=${this.email}&password=${this.password}`
            );
            let result = await request.data;
            if (request.status == 200 && result.length == 0) {
                document.getElementById("loginErr").style.display = "block";
            } else {
                this.$router.push({ name: "Home" });
                localStorage.setItem("user-info", JSON.stringify({
                    email: result[0].email,
                    name: result[0].name
                }));
            }
        },
        loginCheck() {
            const auth = localStorage.getItem("user-info");
            if (auth) {
                this.$router.push({ name: "Home" });
            }
        }
    }
}
</script>
<style>
* {
    padding: 0;
    margin: 0;
    box-sizing: border-box;
}

p {
    margin-left: 70px;
}

p.login-error {
    display: none;
    color: red;
    margin-bottom: 10px;
}
</style>