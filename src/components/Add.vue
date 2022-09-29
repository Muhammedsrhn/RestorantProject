<template lang="tr">
    <img src="../assets/logo.png" />
    <h1>Add Restorant</h1>
    <div class="form">
        <input type="text" placeholder="Enter a Name" v-model="name" ref="name">
        <input type="text" placeholder="Enter a Contact" v-model="contact" ref="contact">
        <input type="text" placeholder="Enter a Address" v-model="adress" ref="adress">
        <button class="btn" v-on:click="addRest">Add</button>
        <p>
            <router-link to="/">
                Back
            </router-link>
        </p>
    </div>
</template>
<script>
import axios from 'axios';

export default {
    name: "Add",
    data() {
        return {
            resturant: {
                name: "",
                contact: "",
                adress: "",
            }
        }
    },
    methods: {

        async addRest() {

            let request = await axios.post("http://localhost:3000/restorants", {
                name: this.name,
                contact: this.contact,
                adress: this.adress
            })
            this.$refs['name'].value = "";
            this.$refs['contact'].value = "";
            this.$refs['adress'].value = "";

            let response = await request.data;
            console.warn(response);


        }
    },
    go() {
        const auth = localStorage.getItem("user-info");
        if (!auth) {
            this.$router.push({ name: "Login" });
        }
        alert(21)
    }
}
</script>
<style>
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box
}
</style>