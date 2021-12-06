<template>
    <Home />
</template>
<script>
export default {
  name: 'App',
  data () {
    return {
      User: [],
      error: null
    }
  },
  async mounted () {
    try {
      this.User = await this.$strapi.$User.find()
      console.log(this.User)
    } catch (error) {
      this.error = error
      console.error(error)
    }
  },
  
}
</script>