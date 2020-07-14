<template>
  <div class="hello">
    <h1>{{ fields.home_title }}</h1>
    <prismic-image class="iceCream" :field="fields.image" />
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  components: {},
  data() {
    return {
      fields: {
        home_title: '',
        richtext: null,
        image: null,
      },
    }
  },
  props: {
    msg: String,
  },
  methods: {
    async getContent() {
      const page = await this.$prismic.client.getSingle('homepage')
      const data = page.data
      this.fields.home_title = data.home_title[0].text
      this.fields.richtext = data.richtext
      this.fields.image = data.image
    },
  },
  created() {
    this.getContent()
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.iceCream {
  width: 100%;
}
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
