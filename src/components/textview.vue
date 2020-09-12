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
  background: antiquewhite;
}

</style>