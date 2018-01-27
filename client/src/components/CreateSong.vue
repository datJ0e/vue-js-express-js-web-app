<template>
  <v-layout>
    <v-flex xs4>
      <panel title ="Song Metadata">
        <v-text-field
        label = "Title"
        required
        :rules=[required]
        v-model="song.title">
        </v-text-field>

        <v-text-field
        label = "Artist"
        required
        :rules=[required]
        v-model="song.artist">
        </v-text-field>

        <v-text-field
        label = "Genre"
        required
        :rules=[required]
        v-model="song.genre">
        </v-text-field>

        <v-text-field
        label = "Album"
        required
        :rules=[required]
        v-model="song.album">
        </v-text-field>

        <v-text-field
        label = "Album Image Url"
        required
        :rules=[required]
        v-model="song.albumImageUrl">
        </v-text-field>

        <v-text-field
        label = "Youtube Id"
        required
        :rules=[required]
        v-model="song.youtubeId">
        </v-text-field>
      </panel>
  </v-flex>

  <v-flex  xs8>
    <panel title="Song Structure" class="ml-4">
    <v-text-field
     label = "Lyrics"
     required
     :rules=[required]
     multi-line
     v-model="song.lyrics">
     </v-text-field>

     <v-text-field
     label = "Tab"
     required
     :rules=[required]
     multi-line
     v-model="song.tab">
     </v-text-field>
   </panel>
   <v-alert
      class="ml-4"
      :value="error"
      transition="scale-transition"
      error>
      {{error}}
    </v-alert>
    <v-btn class="teal accent-4" @click="create">
     Add Song
   </v-btn>
  </v-flex>
</v-layout>
</template>

<script>
import Panel from '@/components/Panel'
import SongsService from '@/services/SongsService'
export default {
  data () {
    return {
      song: {
        title: null,
        artist: null,
        genre: null,
        album: null,
        albumImageUrl: null,
        youtubeId: null,
        lyrics: null,
        tab: null
      },
      required: (value) => !!value || 'Required.',
      error: null
    }
  },
  components: {
    Panel
  },
  methods: {
    async create () {
      this.error = null
      const areAllFieldsFilled = Object
        .keys(this.song)
        .every(key => !!this.song[key])
      if (!areAllFieldsFilled) {
        this.error = 'Please fill in all the required fields'
        return
      }
      try {
        await SongsService.post(this.song)
        this.$router.push({name: 'songs'})
      } catch (err) {
        console.log(err)
      }
    }
  }
}
</script>

<style scoped>
</style>
