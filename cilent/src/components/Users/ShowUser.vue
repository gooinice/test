<template>
    <div>
        <h1>ข้อมูลผู้รับฝาก</h1>
        <p>ID : {{ user.id }} </p>
        <p>name : {{user.name}}    {{user.lastname}}</p>
        <p>Email : {{user.email}} </p>
        <p>Password : {{user.password}}</p>
    </div>
</template>
<script>
import UsersService from '@/services/UsersService'
export default {
    data() {
        return {
            user: null,
        };
    },
    async created() {
        try {
            let userId = this.$route.params.userId;
            this.user = (await UsersService.show(userId)).data
        } catch (error) {
            console.log(error);
        }
    },
};
</script>
<style scoped>
</style>