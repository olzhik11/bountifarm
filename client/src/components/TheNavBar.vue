<template>
  <div class="navbar">
    <div class="left">
      <TheBaseButton :type="'text'" @click="$router.push('/')">Home</TheBaseButton>
    </div>
    <div class="right">
      <TheBaseButton
      >ITunes Search</TheBaseButton>
    </div>
  </div>
</template>

<script>
import TheBaseButton from "./UI/TheBaseButton";
export default {
  name: "TheNavBar",
  components: {TheBaseButton},

}
</script>

<style scoped>
.navbar{
  display: flex;
  justify-content: space-between;
  border-bottom: 1px solid black;
  width: 100%;
}
</style>