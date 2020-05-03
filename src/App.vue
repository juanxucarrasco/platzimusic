<template lang="pug">
  #app
    img(src='./assets/logo.png')
    h1 JuanxoMusic
    select(v-model="selectedCountry")
      option(v-for="country in countries" v-bind:value="country.value") {{ country.name }}
    ul
      artist(v-for="artist in artists" v-bind:artist="artist")    
</template>

<script>

import Artist from './components/Artist.vue'
import getArtists from './api'

export default {
  name: 'app',
  data () {
    return {
      artists: [],
      countries: [
        { name: 'Perú', value: 'peru' },
        { name: 'España', value: 'spain' },
        { name: 'Colombia', value: 'colombia' },
      ],
      selectedCountry: 'peru'
    }
  },
  components: {
    Artist
  },
  methods: {
    refreshArtists() {
      const self = this
      getArtists(this.selectedCountry)
        .then(function (artists) {
          self.artists = artists
        })
    }
  },
  mounted: function() {
    this.refreshArtists()
  },
  watch: {
    selectedCountry: function() {
      this.refreshArtists()
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
  color #f50057
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
  color #42b983
</style>
