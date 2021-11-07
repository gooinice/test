<template>
    <div>
        <h2> ข้อมูลลูกค้า </h2>

        <!-- <p><button v-on:click="logout" > Logout </button></p> -->

        <h4> จำนวนรถที่ฝาก {{blogs.length}}</h4>
        <p><button v-on:click="navigateTo('/blog/create')"> + เพิ่ม </button></p>
        <div v-for="blog in blogs" v-bind:key="blog.id">
            <p>id: {{ blog.id }} </p>
            <p>ชื่อลูกค้า: {{ blog.title }} </p>
            <p>รายละเอียดรถ: {{ blog.content }} </p>
            <p>วันที่ฝาก: {{ blog.category }} </p>
            <p>ชื่อพนักงาน: {{ blog.status }} </p>
            <p>
                <button v-on:click="navigateTo('/blog/'+ blog.id)"> ดูข้อมูล </button>
                <button v-on:click="navigateTo('/blog/edit/'+ blog.id)"> แก้ไขข้อมูล </button>
                <button v-on:click="deleteBlog(blog)"> ลบข้อมูล </button>
            </p>
            <hr>
        </div>
    </div>
</template>
<script>
import BlogsService from '@/services/BlogsService'
export default {
    data () {
        return { 
            blogs: []
        }
    },
    async created () {
        this.blogs = (await BlogsService.index()).data
    },
    methods: {
       /*  logout () {
            this.$store.dispatch('setToken', null)
            this.$store.dispatch('setBlog', null)
            this.$router.push({
                name: 'login'
            })
        }, */
        navigateTo (route) {
            this.$router.push(route)
        },
        async deleteBlog (blog) {
            let result = confirm("Want to delete?")
            if (result) {
                try {
                    await BlogsService.delete(blog)
                    this.refreshData()
                } catch (err) {
                    console.log(err)
                }
            }
        },
        async refreshData() {
            this.blogs = (await BlogsService.index()).data
        }
    }
}
</script>
<style scoped>
</style>