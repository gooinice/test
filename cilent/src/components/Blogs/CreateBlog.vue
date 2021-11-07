<template>
    <div>
        <h1> เพิ่มข้อมูล </h1>
        <form v-on:submit.prevent = "createBlog">
            <p>ชื่อลูกค้า: <input type="text" v-model="blog.title"></p>
            <p>รายละเอียดรถ: <input type="text" v-model="blog.content"></p>
            <p>วันที่ฝาก: <input type="text" v-model="blog.category"></p>
            <p>ชื่อพนักงาน: <input type="text" v-model="blog.status"></p>
            <p><button type="submit">บันทึกข้อมูล</button></p>
            
        </form>
    </div>
</template>
<script>
import BlogsService from '@/services/BlogsService'
export default {
    data () {
        return { 
            blog: {
                title: '',
                thumbnail: 'null',
                pictures: 'null',
                content: '',
                category: '',
                status: 'saved'
            }
        }
    },
    methods: {
        async createBlog () {
            try {
                await BlogsService.post(this.blog)
                this.$router.push({
                    name: 'blogs'
                })
            } catch (err) {
                console.log(err)
            }
        }
    }
}
        
</script>
<style scoped>
</style>