<template>
  <div>
    <v-container class="grey lighten-5">
      <v-row no-gutters>
        <v-col cols="12" sm="6" md="6">
          <v-card class="pa-2" outlined tile>
            <v-img
              width="400px"
              height="400px"
              :src="this.$route.params.id.artworkUrl100"
            ></v-img>
          </v-card>
        </v-col>
        <v-col cols="6" md="6">
          <v-card class="pa-2" height="100%" text-center outlined tile>
            เพลง : {{ this.$route.params.id.trackName }}<br />
            ศิลปิน : {{ this.$route.params.id.artistName }}<br />
            แนวเพลง : {{ this.$route.params.id.primaryGenreName }}<br /><br />
            <contener>
              <audio controls>
                <source
                  :src="this.$route.params.id.previewUrl"
                  type="audio/mpeg"
                />
              </audio>
            </contener>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>

<script>
export default {}
</script>

<style>
</style>