<template>
  <div>
    <nuxt-link
      v-for="locale in availableLocales"
      :key="locale.code"
      :to="switchLocalePath(locale.code)">
      {{ locale.name }}
    </nuxt-link>
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
  computed: {
    availableLocales () {
      return this.$i18n.locales.filter(i => i.code !== this.$i18n.locale)
    }
  },
  async fetch() {
    try{
      this.blogs = await this.$strapi.$blogs.find({_locale: this.$i18n.locale})
    }catch(error){
      this.error = error
    }
  }
}
</script>
