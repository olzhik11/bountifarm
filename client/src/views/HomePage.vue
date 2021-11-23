<template>
  <div class="homePage">
    <TheNavBar  />
    <TheBaseInput @song="getSong"  />
      <TrackItem
          v-for="result in results" :key="result.id" :result="result"
      />
  <div ref="observer" class="observer"></div>
    <div v-if="noResult" class="results">No results found...</div>
  <div v-if="end" class="end">End of the list</div>
  </div>
</template>
<script>

import TheBaseInput from "@/components/UI/TheBaseInput";
import TrackItem from "@/components/UI/TrackItem";
import axios from 'axios'
import TheNavBar from "@/components/TheNavBar";
export default {
  name: 'Home',
  components: {
    TheNavBar,
    TrackItem,
    TheBaseInput
  },
  data(){
    return{
      observer: null,
      results: [],
      flag: false,
      offset: 0,
      songTitle: '',
      end: false,
      noResult: false
    }
  },
  methods:{
    async getSong(event){
      this.results = []
      this.end = false
      this.offset = 0
      this.songTitle = event
      this.flag = false
      this.noResult = false
      await this.returnSongs()
    },
    async returnSongs(){
      axios.get(`https://itunes.apple.com/search?term=${this.songTitle}&entity=song`, {
        params: {
          limit: 10,
          offset: this.offset
        }
      })
      .then((res) => {
        this.results = [...this.results, ...res.data.results]
        if (res.data.results.length === 0 && this.results.length === 0) {
          this.noResult = true
          return
        }
        if (res.data.results.length < 10) {
          this.end = true
          this.observer.disconnect()
        }
        if (!this.flag){
          this.flag = true
          const options = {
            rootMargin: '0px',
            threshold: 1.0
          }
          const callback = (entries) => {
            if (entries[0].isIntersecting) {
              this.offset += 11
              this.returnSongs()
            }
          }
          this.observer = new IntersectionObserver(callback, options)
          this.observer.observe(this.$refs.observer)
        }
      })
      .catch((err) => {console.log(err)})
    },
  },

}
</script>
<style scoped>
.homePage{
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
.observer{
  height: 5px;
  background: black;
}
.end{
  margin: 5px;
  border: 2px solid;
  border-radius: 10px;
  padding: 5px;

}

</style>