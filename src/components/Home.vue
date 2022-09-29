<template lang="tr">
    <div class="home">
        {{get()}}
        <h1>Welcome To Home Page {{name}}</h1>
        <table>
            <tr>
                <td class="th-title">ID</td>
                <td  class="th-title">Name</td>
                <td  class="th-title" >Contact</td>
                <td  class="th-title">Adress</td>
                <td  class="th-title">Actions</td>
            </tr>
            <tr class="my" v-for="item in resturants" key="{{item.id}}">
            <td>{{item.id}}</td>
            <td>{{item.name}}</td>
            <td>{{item.contact}}</td>
            <td>{{item.adress}}</td>
            <td><router-link :to="'/update/'+item.id">Update</router-link>
            <button v-on:click="deleteRest(item.id)" class="btn-delete">Delete</button>
            </td>
            </tr>
        </table>
        
    </div>
</template>
<script>
import axios from 'axios';

export default {
    name: "Home",
    data() {
        return {
            name: '',
            resturants: []
        }
    },

    methods: {
        deleteRest(id) {
            const control = confirm("Delete?");
            if(control){
                axios.delete("http://localhost:3000/restorants/" + id)
                .then(e => console.warn(e));
            }
    
        },
        get() {
            let auth = localStorage.getItem("user-info");
            this.name = JSON.parse(auth).name
            if (!auth) {
                this.$router.push({ name: "Login" });
            }
            axios.get("http://localhost:3000/restorants")
                .then(result => {
                    this.resturants = result.data;
                })
        }
    }

}
</script>
<style>
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box
}

.home {
    text-align: center;
    width: 100%;
}

.btn-delete {
    background-color: red;
    border: none;
    color: #fff;
    padding: 5px;
    margin: 5px;
}

.btn-delete:hover {
    opacity: 0.6;
}

table,
tr,
td {
    border: none;
    border-collapse: collapse;
    margin-left: 20%;
}

tr,
th {
    padding: 18px;
    font-size: 20px;
    background-color: rgb(159, 159, 132);
    color: #fff;
}

tr.my:hover {
    background-color: black;
    border: 1px solid #fff;
}


.th-title {
    background-color: rgb(34, 249, 34);
    color: #fff;
    padding: 5px;
    font-size: 20px;
}

table {
    width: 800px;
    height: 120px;
}

a {
    text-decoration: none;
    color: #fff;
}

a:hover {
    opacity: 0.5;
}

@media only screen and (max-width:800px) {
    table {
        width: 400px;
        margin-left: 20%;
    }

    tr,
    th {
        padding: 17px;
        font-size: 10px;
        background-color: rgb(159, 159, 132);
        color: #fff;
    }
}
</style>