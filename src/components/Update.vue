<template lang="tr">
    <img src="../assets/logo.png" />
    <h1>Update Restorant</h1>
    <div class="form">
        <input type="text" placeholder="Enter a Name" v-model="user" ref="name">
        <input type="text" placeholder="Enter a Contact" v-model="contact" ref="contact">
        <input type="text" placeholder="Enter a Address" v-model="adress" ref="adress">
        <button class="btn" v-on:click="addUpdate">Add</button>
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
    name: "Update",
    // data() {
    //     return {
    //         resturant: {
    //             name: "",
    //             contact: "",
    //             adress: "",
    //         }
    //     }
    // },
    methods: {
        async addUpdate() {
            let request = await axios.put("http://localhost:3000/restorants/" + this.$route.params.id, {
                name: this.user,
                contact: this.contact,
                adress: this.adress
            });
            let response = await request.data;
            console.log(response);
        }
    },

    async mounted() {
        const auth = localStorage.getItem("user-info");
        if (!auth) {
            this.$router.push({ name: "Login" });
        }
        //cath params sending url
        axios.get("http://localhost:3000/restorants?id=" + this.$route.params.id)
            .then(result => {
                this.$refs["name"].value = result.data[0].name;
                this.$refs["contact"].value = result.data[0].contact;
                this.$refs["adress"].value = result.data[0].adress;
                console.log(result.data);
                this.resturant = result.data;
            })
            .catch(e => console.log(e));
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