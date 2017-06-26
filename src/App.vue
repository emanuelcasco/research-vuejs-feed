<template lang="pug">
  #app
    .container
      img(src='dist/logo.png')
      h1 VUE ES LO MAS
      h2 Last.fm API
      select(v-model="selectedCountry")
        option(v-for="country in countries" :value="country.value") {{ country.name }}
      spinner(v-show="loading")
      ul
        .row
          artist(v-for="artist in artists" :artist="artist" :key="artist.mbid")
</template>

<script>
import Artist from './components/Artist.vue'
import Spinner from './components/Spinner.vue'
import getArtists from './api'

export default {
  name: 'app',
  data () {
    return {
      artists: [],
      countries: [
        { name: 'Argentina', value: 'argentina' },
        { name: 'Colombia', value: 'colombia' },
        { name: 'España', value: 'spain' },
      ],
      selectedCountry: "argentina",
      loading: true
    }
  },
  components: {
    Artist,
    Spinner
  },
  methods: {
    refreshArtists() {
      const self = this;
      this.loading = true;
      this.artists = [];
      getArtists(this.selectedCountry)
      .then(function (artists) {
        self.loading = false;
        self.artists = artists;
      });
    }
  },
  mounted() {
    this.refreshArtists();
  },
  watch: {
    selectedCountry() {
      this.refreshArtists();
    }
  }
}
</script>

<style lang="stylus">
#app
  font-family 'Avenir', Helvetica, Arial, sans-serif
  -webkit-font-smoothing antialiased
  -moz-osx-font-smoothing grayscale
  text-align center
  color #2c3e50
  margin-top 60px

h1, h2
  font-weight normal

ul
  list-style-type none
  padding 0

li
  display inline-block
  margin 0 10px

a
  color #2c3e50
  font-weight bold
</style>
