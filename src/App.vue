<template>
  <div id="app">
    <!--<img src="./assets/logo.png">-->
    <appCatalog>

    </appCatalog>
  </div>
</template>

<script>

  import appCatalog from './components/catalog'

  export default {
    name: 'catalogPage',
    data () {
      return {
        msg: 'Welcome to Your Vue.js App',
      }
    },
    components: {
      appCatalog,
    }
  }
</script>

<style lang="sass">
/*bootstrap styles*/
@import "assets/sass/vars"
@import '../node_modules/bootstrap/scss/bootstrap'
@import "assets/sass/fonts"

*
  font-family: $default-font
  outline: none!important

html, body
  height: auto
body
  font-size: 16px
  min-width: 1280px
  position: relative
  line-height: 1.2
  font-family: $default-font
  opacity: 1
  margin: 0px
  background: $white


</style>
