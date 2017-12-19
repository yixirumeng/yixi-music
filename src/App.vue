<template>
  <div id="app">
    <m-header></m-header>
  </div>
</template>

<script>
    import MHeader from '@/components/m-header/m-header'

    export default{
      components: {
        MHeader
      }
    }
</script>

<style lang="scss" scoped>
@import "./common/styles/variable";

#app{
  color: $color-theme;
}
</style>
