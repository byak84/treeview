<template>
  <div class="textview">
    <textarea>{{ text }}</textarea>
  </div>

</template>


<script>
export default {
  props: ['text'],
  data: () => {
    return {
      checked: false,
    }
  }

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
  width: 99%;
  height: 99%;
  font-family: Verdana, Tahoma, Arial;
  border: 3px solid #888;
  resize: none;
}

</style>