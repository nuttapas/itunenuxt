<template>
  <div>
    <br />
    <center>
      <span class="mdi mdi-magnify"></span>
      <input
        type="text"
        name="searchInput"
        id="searchInput"
        placeholder="Search"
        v-model="textInput"
      />
      <button @click="getitem()" elevation="2">Search</button>
    </center>
    <v-chip-group column>
    <v-card 
      v-for="list in tmp"
      :key="list.trackId"
      class="mx-auto"
      max-width="344"
    >

      <v-img :src="list.artworkUrl100" height="200px"></v-img>

      <v-card-title>
        {{ list.trackName }}
      </v-card-title>


      <v-card-actions>
        <v-btn
          :to="{ name: 'id-id', params: { id: list } }"
          color="orange lighten-2"
          text
        >
          See more
        </v-btn>

        <v-spacer></v-spacer>

        <v-btn icon @click="show = !show">
          <v-icon>{{ show ? 'mdi-chevron-up' : 'mdi-chevron-down' }}</v-icon>
        </v-btn>
      </v-card-actions>

      <v-expand-transition>
        <div v-show="show">
          <v-divider></v-divider>
        </div>
      </v-expand-transition>
    </v-card>
    </v-chip-group>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  data() {
    return {
      textInput: '',
      tmp: null,
    }
  },
  methods: {
    getitem() {
      axios
        .get(
          'https://itunes.apple.com/search?term=' + this.textInput + '&limit=30'
        )
        .then((response) => {
          this.tmp = response.data.results
          console.log(response.data.results)
        })
    },
  },
}
</script>

<style>
</style>