<!--Каталог компонент-->
<template>
  <div class="container">
    <div class="row">
      <div class="col-12">
        <h1>
          ComponentTemplate {{msg}}
        </h1>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'catalog',
    data () {
      return {
        msg: 'template'
      }
    },
    computed: {
    },
    props: [],
    methods: {
    },
  }
</script>

<style lang="sass">

</style>
