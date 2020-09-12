<template>
<div class="treeview">
  <ul class="root_ul">
    <category v-for="(newsArray,cat) in tree"
              :key="newsArray.id"
              v-bind:title="cat"
              v-bind:newsArray="newsArray"
              v-on:itemclick="itemclick"
    />
  </ul>
</div>
</template>

<script>
import Category from "@/components/category";

export default {
  components: {Category},
  props: ['tree'],
  methods: {
    itemclick: function (path) {
      this.$emit("itemclick", path);
    }
  }
}
</script>

<style scoped>

.treeview {
  padding: 0px;
  width: 30%;
  height: 100%;
  background-color: aquamarine;
  float: left;
}

.root_ul {
  margin: 0;
  padding: 0;
  list-style-type: none;
}

</style>