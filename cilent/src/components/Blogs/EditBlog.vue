<template>
  <div>
    <h1>แก้ไขข้อมูล</h1>
    <form v-on:submit.prevent="editBlog">
      <p>ชื่อลูกค้า: <input type="text" v-model="blog.title" /></p>
      <p>รายละเอียดรถ: <input type="text" v-model="blog.content" /></p>
      <p>วันที่ฝาก: <input type="text" v-model="blog.category" /></p>
      <p>ชื่อพนักงาน: <input type="text" v-model="blog.status" /></p>
      <p>
        <button type="submit">บันทึกข้อมูล</button>
        <button v-on:click="navigateTo('/blogs')">กลับ</button>
      </p>
    </form>
  </div>
</template>
<script>
import BlogsService from "@/services/BlogsService";
export default {
  data () {
    return {
      blog: {
        title: "",
        thumbnail: "null",
        pictures: "null", 
        category: "",
        status: "",
      },
    };
  },
  methods: {
    async editBlog() {
      try {
        await BlogsService.put(this.blog);
        this.$router.push({
          name: "blogs",
        });
      } catch (err) {
        console.log(err);
      }
    },
  },
  async created() {
    try {
      let blogId = this.$route.params.blogId;
      this.blog = (await BlogsService.show(blogId)).data;
    } catch (error) {
      console.log(error);
    }
  },
};
</script>
<style scoped>
</style>