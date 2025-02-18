<template>
  <div class="p-5">
    <h1 class="title text-center pb-3">Listen here</h1>
    <SongRecommendation :songs='songs'/>

    <div class="container-lg text-center">
      <button v-if="!editing" class="btn btn-success" @click="editing = true">Add new song</button>
      <button v-else @click="editing=false" class="btn btn-danger">Cancel</button>
      <div v-if="editing">
        <form class="row my-2 justify-content-center">
          <div class="col-sm-7 my-2">
            <label for="songTitle" class="form-label fs-4 lead">Title</label>
            <div class="input-group justify-content-center">
              <span class="input-group-text">
                <i class="bi bi-file-music"></i>
              </span>
              <input class="form-control" id="songTitle" type="text" placeholder="Title" v-model="newSong.title">
            </div>
          </div>

          <div class="col-sm-7 my-2">
            <label for="artist" class="form-label fs-4 lead">Artist</label>
            <div class="input-group justify-content-center">
              <span class="input-group-text">
                <i class="bi bi-file-person"></i>
              </span>
              <input class="form-control" id="artist" type="text" placeholder="Artist" v-model="newSong.artist">
            </div>
          </div>

          <div class="col-sm-7 my-2">
            <label for="coverPhoto" class="form-label fs-4 lead">Cover photo</label>
            <div class="d-flex justify-content-center">
              <input class="mx-auto" type="file" @change="handleFile">
            </div>
          </div>
        </form>
        <button class="btn btn-success" @click="addSong">Add song</button>
      </div>
    </div>
</div>
</template>

<script>
import SongRecommendation from '../../music-recommendations-bootstrap/src/components/SongRecommendation.vue';


export default {
  data() {
    return{
      songs: [
        {
          id: 1,
          title: "Chicken Fried",
          artist: "Zac Brown Band",
          img: "Covers\\Zac Brown Band - Chicken Fried.PNG",
          isFavorite: true
        },
        {
          id: 2,
          title: "Take Me Home, Country Roads",
          artist: "John Denver",
          img: "Covers\\John Denver - Take me Home, Country Roads.PNG",
          isFavorite: false
        },
        {
          id: 3,
          title: "Jolene",
          artist: "Dolly Parton",
          img: "Covers\\Dolly Parton - Jolene.PNG",
          isFavorite: false
        },
        {
          id: 4,
          title: "Tennessee Whiskey",
          artist: "Chris Stapleton",
          img: "Covers\\Chris Stapleton - Tennessee Whiskey.PNG",
          isFavorite: false
        },
        {
          id: 5,
          title: "Wagon Wheel",
          artist: "Old Crow Medicine Show",
          img: "Covers\\Old Crow Medicine Show - Wagon Wheel.PNG",
          isFavorite: false
        },
        {
          id: 6,
          title: "Friends in Low Places",
          artist: "Garth Brooks",
          img: "Covers\\Garth Brooks - Friends in Low Places.PNG",
          isFavorite: false
        }
      ],
      editing: false,
      newSong: {
        id: 7,
        title: '',
        artist: '',
        img: '',
        isFavorite: false
      },
      
    }
  },
  methods: {
        handleFile(event){
          const file = event.target.files[0]
          if(file){
            this.newSong.img = URL.createObjectURL(file)
          }
        },
        addSong(){
          this.songs.push(this.newSong)
          this.newSong = {artist: '', title: ''}
          this.editing = false
        },
       
        getRecommendation(){
          this.recommend = true
        }
      },
  components: {SongRecommendation}
}
</script>


<style>

</style>
