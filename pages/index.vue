<template>
  <div>
    <h1>Nuxt Strapi</h1>
    <article v-for="blog in blogs" :key="blog._id">
      <h2>{{ blog.title }}</h2>
      <p>{{ blog.body }}</p>
    </article>
  </div>
</template>

<script>
export default {
  data(){
    return{
      blogs:[],
      error: ''
    }
  },
  async mounted() {
    try{
      this.blogs = await this.$strapi.$blogs.find({_locale:'tr'})
    }catch(error){
      this.error = error
    }
  }
}
</script>
