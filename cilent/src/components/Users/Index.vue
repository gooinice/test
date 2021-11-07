<template>
<div>
    <h1>ผู้รับฝาก</h1>
    <div v-if="users.length">
        <h4>จำนวนผู้ใช้ {{users.length}}</h4>
        <p><button v-on:click="navigateTo('/user/create')"> + เพิ่ม </button></p>
        <div v-for="user in users" v-bind:key="user.id">
            <p>ID : {{user.id}}</p>
            <p>name : {{user.name}}    {{user.lastname}}</p>
            <p>Email : {{user.email}}</p>
            <p>Password : {{user.password}}</p>
            <p><button v-on:click="navigateTo('/user/'+user.id)">ดูข้อมูล</button>
               <button v-on:click="navigateTo('/user/edit/'+user.id)">แก้ไขข้อมูล</button>
               <button v-on:click="deleteUser(user)">ลบข้อมูล</button></p>
            <hr>
        </div>
        <p><button v-on:click="logout">Logout</button></p>
    </div>
</div>
</template>
<script>
import UsersService from '@/services/UsersService';
export default {
    data(){
        return {
            users:[]
        }
    },
    async created() {
        try {
            this.users = (await UsersService.index()).data;
        } catch (error) {
            console.log(error);
        }
    },
    methods:{
        navigateTo(route){
            this.$router.push(route)
        },
        async deleteUser(user){
            let result = confirm("Want to delete")
            if(result){
                try{
                    await UsersService.delete(user)
                    this.refreshData()
                } catch(error){
                    console.log(error)
                }
            }
        },
        async refreshData () {
            this.users = (await UsersService.index()).data
        },
        logout(){
             this.$store.dispatch('setToken',null)
             this.$store.dispatch('setUser',null)
             this.$router.push({
                 name: 'login'
             })
         }
    },
};
</script>
<style scoped>
</style>