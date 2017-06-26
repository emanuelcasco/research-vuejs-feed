<template lang="pug">
  .col.s6.m3
    .card
      .card-image
        img(:src="artist.image[2]['#text']")
        span: a(:href="artist.url" target="_blank") {{ artist.name }}
</template>

<script>
export default {
  name: 'artist',
  props: [ 'artist' ]
}
</script>

<style lang="stylus" scoped>
li.artist
  display block
  margin 10px 0
</style>
