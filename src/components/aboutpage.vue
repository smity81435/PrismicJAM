<template>
  <div class="about">
    <prismic-rich-text v-if="fields.title" class="" :field="fields.title" wrapper="h1" />
    <prismic-rich-text v-if="fields.richtext" class="" :field="fields.richtext" wrapper="h1" />
    <prismic-image v-if="fields.image" class="aboutpic" :field="fields.image" />
  </div>
</template>

<script>
export default {
  name: 'about',
  data() {
    return {
      fields: {
        title: null,
        image: null,
        richtext: null,
      },
    }
  },
  methods: {
    async getContent() {
      const page = await this.$prismic.client.getSingle('aboutpage')
      const data = page.data
      this.fields.title = data.aboutheader
      this.fields.richtext = data.aboutcontent
      this.fields.image = data.aboutpic
    },
  },
  created() {
    this.getContent()
  },
}
</script>

<style lang="scss" scoped>
.aboutpic {
  width: 100%;
}
</style>
