<template>
  <Header />
  <router-view />
</template>

<script>
import Header from './components/Header.vue';


export default {
  name: "App",
  components: { Header }
}

</script>

<style>
* {
  font-family: 'Open Sans', sans-serif;
}

#app {
  text-align: center;

}

input {
  display: block;
  margin-left: 43%;
  margin-bottom: 15px;
  padding: 10px;
  font-size: 18px;
}

.btn {
  color: #fff;
  background-color: green;
  border: none;
  padding: 10px;
  height: 40px;
  margin-left: 42.9%;
  border-radius: 5px;
  display: block;
  width: 240px;
  margin-bottom: 15px;
}


.btnSign:hover {
  background-color: #fff;
  color: black;
}

.form {
  position: fixed;
  width: 100%;
  height: 100vh;
}

img {
  width: 100px;
  margin-bottom: 15px;
  margin-left: 60px;
}

input:focus {
  outline: none;
}

.btn:hover {
  background-color: #fff;
  border: 1px solid green;
  color: black;
}

h1 {
  margin-bottom: 15px;
  margin-left: 60px;
}

@media only screen and (max-width: 600px) {
  img {
    width: 90px;
    margin-left: 150px;
  }

  h1 {
    margin-left: 145px;
  }

  .ı {
    margin-left: 155px;
  }
}
</style>
