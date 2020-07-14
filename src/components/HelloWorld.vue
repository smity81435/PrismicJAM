<template>
  <div class="hello">
    <h1>{{ fields.home_title }}</h1>
    <prismic-image class="blackCat" :field="fields.image" />
    <prismic-rich-text class="homeexplain" :field="fields.richtext" />
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
// Scoping
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.blackCat {
  position: fixed;
  z-index: -1;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}
.hello {
  padding: 4.5rem 5%;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  height: 30rem;
}
.hello > h1 {
  color: white;
  font-weight: 300;
}
.homeexplain {
  color: white;
  font-weight: 600;
  width: 75%;
  margin: 0 auto;
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
