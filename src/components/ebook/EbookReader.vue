<template>
  <div class="ebook-reader">
    <div class="read"></div>
  </div>
</template>

<script>
  import { mapGetters } from 'vuex'
  import Epub from 'epubjs'
  global.epub = Epub
  export default {
    computed: {
      ...mapGetters(['fileName'])
    },
    methods: {
      initEpub () {
        const url = 'http://192.168.1.103:8081/epub/' + this.fileName + '.epub'
        console.log(url)
        this.book = new Epub(url)
        console.log(this.book)
      }
    },
    mounted () {
      const fileName = this.$route.params.fileName.split('|').join('/')
      this.$store.dispatch('setFileName', fileName).then(() => {
        this.initEpub()
      })
    }
  }
</script>

<style lang="scss" ref="stylesheet/scss" scoped>
  @import "../../assets/styles/global";
</style>
