<template>
  <div class="input-ui">
  <input
      v-model="songTitle"
      class="input"
      type="text"
      placeholder="Search..."
      ref="input"
      @keyup.enter="Search"
  />
    <button class="search"
       @click="Search"
    >
      <i class="fas fa-search">
      </i></button>
  </div>
</template>

<script>
export default {
  name: "TheBaseInput",
  components: {},
  data() {
    return{
      songTitle: '',
    }
  },
  methods: {
    Search(){
      this.$emit('song', this.songTitle)
    }
  }
}
</script>

<style scoped>
.input-ui{
  display: flex;
  justify-content: center;
  align-items: center;
  border-radius: 10px;
  border: 2px solid;
  margin: 10px;
  padding: 5px;
}
.input{
  padding: 5px;
  min-width: 50%;
  border: none;
  outline: none;
}

.search{
  background: none;
  border: none;
  cursor: pointer;
  transition: all 0.75s;
}
.search:hover{
  color: #7fe7c4;
}
</style>