<template lang="tr">
    <div class="header">
    <ul>
        <li>
            <router-link to="/">Home</router-link>
        </li>
        <li>
            <router-link to="/add">Add restorant</router-link>
        </li>
        <li>
            <a v-on:click="logout">Logout</a>
        </li>
    </ul>
    </div>
</template>
<script>

export default {
    name: "Header",

    methods: {
        logout() {
            localStorage.clear();
            this.$router.push({ name: "Login" })
        }
    }
}
</script>
<style>
.header {
    margin-bottom: 10px;
    background-color: #444;
    width: 100%;
    height: 60px;
    display: flex;
}

ul {
    width: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
    text-align: center;
}

li {
    display: inline-block;
    text-align: center;
    padding: 10px;
}

li a {
    text-decoration: none;
    color: white;
}

li a:hover {
    color: black;
}
</style>