<template>
  <div class="textview">
<!--    <p id="text">{{text}}</p>-->
    <textarea>{{text}}</textarea>
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
  /*background: antiquewhite;*/
  float: left;
}
textarea {
  width: 100%;
  height: 100%;
}

</style>