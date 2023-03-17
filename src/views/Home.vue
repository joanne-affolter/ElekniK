<template>
  <div>
    <div v-if="song">

    <v-card class="mb-6">
      <v-card-title class = "text-h1">ElecNIK ⚡</v-card-title>
      <v-img src="@/assets/images/doigt-dhonneur.gif"></v-img>
      <audio :src="song.preview_url" controls></audio>
    </v-card>
    </div>
    <div v-else>
      Wait...
    </div>

    </v-card>


  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'Home',
  data() {
    return {
      users: [],
      access: '',
      song: null,
    }
  },
  mounted() {},
  methods: {
    getSong: function () {
      const access_token = this.access
      const headers = {
        Authorization: 'Bearer ' + access_token,
        'Content-Type': 'application/json',
      }
      const query = 'Never Gonna Give You Up' // your song query here
      const type = 'track'
      const url = `https://api.spotify.com/v1/search?q=${query}&type=${type}`

      axios
        .get(url, { headers })
        .then(response => {
          this.song = response.data.tracks.items[0]
          console.log(this.song)
        })
        .catch(error => {
          console.log(error.response.data)
        })
    },
  },
}
</script>
