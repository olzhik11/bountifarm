<template>
  <button class="button" :style="type ? 'border: none;' : 'border: 2px solid;'">
    <slot></slot>
  </button>
</template>

<script>
export default {
  name: "TheBaseButton",
  props: {
    type: String
  }
}
</script>

<style scoped>
.button{
  font-size: 15px;
  padding: 5px;
  margin: 10px;
  background-color: white;
  color: black;
  text-decoration: none;
  text-align: center;
  border-radius: 4px;
  cursor: pointer;
  transition: all 0.75s;
}
.button:hover{
  color: #7fe7c4;
  border-color: #7fe7c4;
}

</style>