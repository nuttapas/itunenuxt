<template>
  <div>
    <v-row>
      <v-col cols="10">
        <v-text-field label="" solo v-model="textSearch"></v-text-field>
      </v-col>
      <v-col cols="2">
        <v-btn @click="search()" large><v-icon>Series-Vote</v-icon></v-btn>
      </v-col>
    </v-row>

    <v-row>
      <v-col v-for="series in seriesList" :key="series.id" :title="series.title">
        <nuxt-link :to="{ name: 'id-id', params: { id: series } }">
          <v-hover v-slot:default="{ hover }">
            <v-card flat tile class="d-flex" :elevation="hover ? 12 : 2">
              <v-img
                :src="movie.poster_path"
                aspect-ratio="1"
                class="grey lighten-2 rounded"
              >
                <p class="font-weight-bold grey" style="color: white">
                  {{ series.title }}
                </p>
              </v-img>
            </v-card>
          </v-hover>
        </nuxt-link>
      </v-col>
    </v-row>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  data() {
    return {
      seriesList: null,
      textSearch: '',
    }
  },
  methods: {
    search() {
      axios
        .get(
          'https://api.themoviedb.org/3/search/tv?api_key=aaf4e31fa3a5803c52aabf3cfde977fc&language=en-US&page=1&query=' +
            this.textSearch
        )
        .then((res) => {
          this.seriesList = res.data.results
          this.$$emit('seriesList', Object(res.data.results))
        })
        .catch((err) => {
          console.log(err)
        })
    },
  },
}
</script>

<style></style>
