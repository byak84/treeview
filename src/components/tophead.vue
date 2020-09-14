<template>
  <div class="header">
    <input type="button" value="Добавить" v-on:click="$emit('showmodal')" />
  </div>
</template>

<script>
export default {
  methods: {
    add: function () {

    }
  }
}
</script>


<style scoped>

.header {
  width: 100%;
  background-color: cornflowerblue;
  margin: 0;
  padding: 0;
}

</style>