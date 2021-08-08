<template>
    <div>
    <h1>show User</h1>
    <p>id: {{ user.Id }}</p>
    <p>ชื่อ - นามสกุล {{ user.name }} - {{ user.lastname }}</p>
    <p>email: {{ user.email }}</p>
    <p>password: {{ user.password }}</p>
    </div>
</template>
<script>
import UsersService from '@/services/UsersService'

export default {
  data() {
    return{
      user: null,
    };
  },
  async created() {
    let userId = this.$route.params.userId;
    this.user = (await UsersService.show(userId)).data
  },
};
</script>
<style scoped>
</style>
