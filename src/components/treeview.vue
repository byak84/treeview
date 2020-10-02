<template>
<div class="treeview">
  <ul class="root_ul">
    <category v-for="(newsArray,cat) in tree"
              :key="newsArray.uuid"
              v-bind:title="cat"
              v-bind:newsArray="newsArray"
              v-on:itemclick="itemclick"
              v-on:deleteItem="deleteItem"
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
    itemclick: function (path, contex) {
      this.$emit("itemclick", path);
      let children = this.$children;
      children.forEach(function (cat, i, children) {
        cat.unselectAll(contex);
      })
    },
    deleteItem: function (uuid, cat) {
      this.$emit("deleteItem", uuid, cat)
    }
  }
}
</script>

<style scoped>

.treeview {
  padding: 0px;
  width: 30%;
  height: 100%;
  /*background-color: #7fffd4;*/
  float: left;
}

.root_ul {
  margin: 0;
  padding: 0;
  list-style-type: none;
}

</style>