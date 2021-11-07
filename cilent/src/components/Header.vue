<template >
  <div>
  <h1> JS Car Service </h1>
    <div class="nv-navbar">
      <ul class="nav">
        <li><router-link :to="{ name: 'blogs' }"> Customer </router-link></li>
        <li><router-link :to="{ name: 'users' }"> Depositary </router-link></li>
        <li><router-link :to="{ name: 'comments' }"> Comments</router-link></li>
        <li><router-link :to="{ name: 'login' }"> Login </router-link></li>
        <li><a v-on:click.prevent="logout" href="#"> Logout </a></li> 
      </ul>
      <div class="clearfix"></div>
    </div>
  </div>
</template>
<script>
export default {
  methods:{
  logout () {
          this.$store.dispatch('setToken', null)
          this.$store.dispatch('setUser', null)
          this.$router.push({
            name: 'login'
    })
    }
  }
}
</script>
<style scoped>


.nv-navbar {
  background-color: rgb(64, 249, 212);
  width: 100%;
  padding: 10px 0px 10px 0px;
}
.nv-navbar .nav {
  list-style: none;
  margin: 0;
  padding: 0;
  float: left;
}
.nv-navbar .nav li {
  float: left;
}
.nv-navbar .nav li a {
  padding: 10px;
  text-decoration: none;
  color: gray;
  font-weight: bold;
}
.nv-navbar .nav li a:hover {
  padding: 10px;
  text-decoration: none;
  color: darkslategrey;
}
.nv-navbar .nav li a.router-link-active {
  background-color: rgb(17, 173, 142);
  color: rgb(0, 0, 0);
}
.clearfix {
  clear: left;
}
</style>