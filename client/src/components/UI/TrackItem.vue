<template>
  <div class="track">
      <div class="left">
    <div  class="img">
      <img :src="result.artworkUrl100" alt="vue">
    </div>
    <div class="description">
      <div class="trackDetails">
        <h4>{{result.trackName}}</h4>
        <p>{{ result.collectionName }}, {{result.releaseDate.substr(0,10)}}</p>
      </div>
      <div class="artistDetails">
        <h5>{{result.artistName}}</h5>
      </div>
    </div>
      </div>
    <p class="duration">{{ returnDuration}}</p>
  </div>
</template>

<script>
export default {
  name: "TrackItem",
   props: {
     result: Object
   },
  computed:{
    returnDuration(){
      const seconds = Math.floor(this.result.trackTimeMillis/1000)
      return Math.floor(seconds/60).toString()
          + ':' + (seconds%60 >= 10 ? (seconds%60).toString() : '0' + (seconds%60).toString())
    }
  }
}
</script>

<style scoped>
.track{
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  border: 2px solid;
  margin: 5px;
  border-radius: 10px;
  width: 40%;
}
.left{
  display: flex;
  flex-direction: row;
}
.img{
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 5px;
}
img{
  border-radius: 10px;
}
.description{
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  margin: 5px 10px 5px 10px;
}
.duration{
  margin: 5px;
}
</style>