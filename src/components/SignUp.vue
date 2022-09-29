<template>
    {{go()}}
    <img src="../assets/logo.png" />
    <h1>Sign Up</h1>
    <div class="form">
        <input type="text" placeholder="Enter a Name" v-model="name">
        <input type="text" placeholder="Enter a Email" v-model="email">
        <input type="password" placeholder="Enter a Password" v-model="password">
        <button class="btn" v-on:click="signUp">Submit</button>
        <p>
            <router-link to="/login">
                Login
            </router-link>
        </p>
    </div>
</template>
<script>
import axios from "axios";
export default {
    name: "SignUp",
    data() {
        return {
            name: '',
            email: '',
            password: ''
        }
    },
    methods: {
        async signUp() {
            let requests = await axios.post("http://localhost:3000/user", {
                name: this.name,
                email: this.email,
                password: this.password
            });

            let response = await requests.data;
            if (requests.status == "201") {
                localStorage.setItem("user-info", JSON.stringify({
                    email: response.email,
                }))
                this.$router.push({ name: "Home" });
            }
        },
        go() {
            const auth = localStorage.getItem("user-info");
            if (auth) {
                this.$router.push({ name: "Home" });
            }
        }
    }
}
</script>
<style>

</style>