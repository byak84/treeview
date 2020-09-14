<template>
  <div class="textview">
    <p id="text">{{text}}</p>
  </div>

</template>


<script>
export default {
  props: ['text'],

}

</script>

<style scoped>

.textview {
  padding: 0px;
  width: 70%;
  height: 100%;
  background: antiquewhite;
  float: left;
}

</style>