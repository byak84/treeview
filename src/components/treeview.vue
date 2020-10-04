<template>
  <div class="treeview">
    <ul class="tree-list">
      <node v-for="node in nodes"
            v-bind:node="node"
            v-bind:key="node.id"
            v-bind:root="true"
      />
    </ul>
  </div>
</template>

<script>
import node from "@/components/node";

export default {
  components: {node},
  props: ['nodes'],
  methods: {}
}
</script>

<style scoped>

.treeview {
  padding: 0px;
  width: 30%;
  height: 100%;
  background-color: #dddddd;
  float: left;
}

.tree-list {
  margin: 0;
  padding: 0;
  user-select: none;
  list-style-type: none;
}

</style>