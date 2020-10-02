<template>
  <div>
    <v-row no-gutters> <nuxt-link to="/"> Home</nuxt-link>/{{ name }} </v-row>
    <v-row nogutters>
      <v-col cols="2">
        <v-img :src="img"></v-img>
      </v-col>
      <v-col cols="8">
        <v-list-item>first air date : {{ first_air_date }}</v-list-item>
        <v-list-item>Average vote : {{ average }}</v-list-item>
        <v-list-item>Overview : {{ overview }}</v-list-item>
      </v-col>
    </v-row>

    <v-row>
      <v-col cols="12">
        <v-card>
          <v-list-item-group>
            <v-list-item v-for="series in seriesList" :key="series.id">
              <v-img :src="series.poster_path" max-width="50"></v-img>
              <p>{{ series.title }}</p>
            </v-list-item>
          </v-list-item-group>
        </v-card>
      </v-col>
    </v-row>
  </div>
</template>

<style></style>

<script>
import axios from 'axios'
export default {
  components: {},
  data() {
    return {
      tmp: null,
      name: this.$route.params.id.name,
      first_air_date: this.$route.params.id.first_air_date,
      overview: this.$route.params.id.overview,
      img: this.$route.params.id.poster_path,
      average: this.$route.params.id.vote_average,
    }
  },
  methods: {
    seeMore() {
      axios
        .get(
          'https://api.themoviedb.org/3/search/tv?api_key=aaf4e31fa3a5803c52aabf3cfde977fc&language=en-US&page=1&query=' +
            this.textSearch
        )
        .then((res) => {
          this.seriesList = res.data.results
          console.log(this.seriesList)
        })
        .catch((err) => {
          console.error(err)
        })
    },
  },
}
</script>
