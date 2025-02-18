<template>
  <div class="justify-content-center text-center">
    <button class="btn btn-warning btn-lg p-3 my-3 fs-4" 
    @click="recommendSong">Get recommendation</button>
    <div v-if="recommendation">
      <div class="mb-3 d-flex justify-content-center"  >
        <div class="d-flex justify-content-center col-12 col-lg-8">
          <div class="card col-6 justify-content-center">
            <img class="card-img-top img-fluid" :src="recommendation.img">
            <div class="card-body">
              <h2>{{ recommendation.title }}</h2>
              <h3>Artist: {{ recommendation.artist }}</h3>

              <div class="card-img-overlay d-flex justify-content-end">
                <div type="button" @click="recommendation.isFavorite = !recommendation.isFavorite">
                  <img v-if="recommendation.isFavorite" src="trueStar.png" class="img-fluid" style="height: 40px; width: 40px;">
                  <img v-else src="falseStar.png" class="img-fluid" style="height: 40px; width: 40px;">
                </div>
              </div>
            </div>
          </div>
          <!-- End of card -->
        </div>
      </div>

      <div>
      <button type="button" class="btn btn-danger mb-3" data-bs-toggle="modal" data-bs-target="#delete-modal">
          Delete song</button>
      </div>

      <div class="modal" id="delete-modal" tabindex="-1">
  <div class="modal-dialog modal-dialog-centered">
    <div class="modal-content bg-dark text-light">
      <div class="modal-header">
        <h5 class="modal-title">Are you sure you want to delete {{ recommendation.title }} by {{ recommendation.artist }} ?</h5>
      </div>

      <div class="modal-body">
        
          <button data-bs-dismiss="modal" class="btn btn-danger btn-lg mx-2" @click="deleteSong(recommendation.id)"> Yes</button>
          <button data-bs-dismiss="modal" class="btn btn-success btn-lg mx-2"> No</button></div>
      </div>
    </div>
  </div>
</div>

      
    <div v-else>Thinking....</div>
  </div>
</template>

<script>

export default {
    props: ['songs'],
    data(){
        return {
            recommendation: null,
            deleting: false
        }
    },
    methods: {
        recommendSong() {
            const randomIndex = Math.floor(Math.random() * this.songs.length)
            this.recommendation = this.songs[randomIndex]
        },
        deleteSong(id) {
          let songToDelete = this.songs.findIndex(song => song.id == id)
          this.songs.splice(songToDelete, 1),
          this.recommendation = null
          this.deleting = false
          // console.log('deleting ' + songToDelete.title + ' by ' + songToDelete.artist)
        }
    },
    }
</script>

<style>

</style>