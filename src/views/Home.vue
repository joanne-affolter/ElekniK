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
  mounted() {
    const axios = require('axios')

    const client_id = '174100d333c649f78b6cdef199fca052'
    const client_secret = '61f3b0453f154b6086cae7ef0af97b33'
    const grant_type = 'client_credentials'
    const url = 'https://accounts.spotify.com/api/token'

    const headers = {
      'Content-Type': 'application/x-www-form-urlencoded',
      Authorization: 'Basic ' + btoa(client_id + ':' + client_secret),
    }

    const data = {
      grant_type: grant_type,
    }

    axios
      .post(url, new URLSearchParams(data), { headers })
      .then(response => {
        const access_token = response.data.access_token
        console.log(access_token)
        this.access = access_token
      })
      .catch(error => {
        console.log(error.response.data)
      })

    this.getSong()
  },
  methods: {
    getSong: function () {
      const access_token = this.access
      const headers = {
        Authorization: 'Bearer ' + access_token,
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
