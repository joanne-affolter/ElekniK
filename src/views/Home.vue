<template>
  <div>
    <v-card class="mb-6">
      <v-card-title class = "text-h1">ElecNIK ⚡</v-card-title>
      <v-img src="@/assets/images/doigt-dhonneur.gif"></v-img>
      <audio :src="song.preview_url" controls></audio>


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
  mounted() {
    this.getSong()
  },
  methods: {
    getSong: function () {
      const access_token =
        'BQDX4RVlSOREaTCTFWje1sH2wbWDOC-pd4nNNIcZvRoDTy80tCfcmVlmH18aDFllWo0hQdBGYr1nbO8BceXfnYtunTlE6eua3B-7HiqFq10jxV4dPiN-'
      const headers = {
        Authorization: 'Bearer ' + 'access_token',
        'Content-Type': 'application/json',
      }
      const query = 'Fuck you' // your song query here
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
