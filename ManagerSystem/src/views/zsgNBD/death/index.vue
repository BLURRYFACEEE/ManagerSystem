<template>
  <div class="death">
    <h2>I SENTENCE TO YOUR DEATH</h2>
    <div class="imgArea">
      <img :src="imgSrc">
    </div>
  </div>
</template>
<script>
export default {
  name: 'Index',
  data() {
    return {
      imgSrc: 'http://chuantu.xyz/t6/741/1608626992x1033348220.gif'
    }
  }
}

</script>

<style scoped>
  .imgArea img {
    display: block;
    width: 30%;
    height: 30%;
    margin: 0 auto;
  }
</style>
