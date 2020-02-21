<template>
  <div>
    <nuxt-link to="/">
      <sui-button
        class="back"
        content="BACK"
        icon="left arrow"
        label-position="left"
        color="red"
      />
    </nuxt-link>
    <div id="detail_conteiner"><img :src="detailRespons.urls.regular" /></div>
  </div>
</template>

<script>
export default {
  async asyncData({ $axios, route }) {
    const detailRespons = await $axios.$get('/photos/' + route.params.id)
    console.log(detailRespons.urls.full)
    return { detailRespons }
  }
}
</script>

<style scoped lang="sass">
#detail_conteiner
  overflow: hidden
  height: 100vh
  img
    width: 100vw
    height: 100%
    object-fit: cover
.back
  position: fixed!important
  left: 10px
  top: 10px
  opacity: .5
  &:hover
    opacity: 1
</style>
