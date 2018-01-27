<template>
  <v-layout column>
    <v-flex xs6 offset-xs3>
      <panel title="Songs">
          <v-btn slot="action" class="cyan accent-4" fab medium light absolute right middle router to="songs/add">
            <v-icon>fa-pencil</v-icon>
          </v-btn>
        <div v-for="song in songs" :key="song.id" class="song">
          <v-layout>
            <v-flex xs6>
              <div class="song-title">
                {{song.title}}
              </div>
              <div class="song-artist">
                {{song.artist}}
              </div>
              <div class="song-genre">
                {{song.genre}}
              </div>
              <v-btn dark class="teal accent-4" @click="navigateTo({name: 'song', params: {songId: song.id}})">
                View
              </v-btn>
            </v-flex>

            <v-flex xs6>
              <img class="album-image" :src="song.albumImageUrl"/>
            </v-flex>
          </v-layout>
      </div>
      </panel>
  </v-flex>
</v-layout>
</template>

<script>
import Panel from '@/components/Panel'
import SongsService from '@/services/SongsService'
export default {
  data () {
    return {
      songs: null
    }
  },
  components: {
    Panel
  },
  async mounted () {
    this.songs = (await SongsService.index()).data
  },
  methods: {
    navigateTo: function (route) {
      this.$router.replace(route)
    }
  }
}
</script>

<style scoped>
.song {
  padding: 20px;
  height: 330px;
  overflow: hidden;
}
.song-title {
  font-size: 30px;
}
.song-artist {
  font-size: 24px;
}
.song-genre {
  font-size: 18px;
}
.album-image {
  width: 70%;
  margin: 0 auto;
}
</style>
