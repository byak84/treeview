<template>
  <div class="treeview">
    <ul class="tree-list">
      <node v-for="node in nodes"
            v-bind:node="node"
            v-bind:key="node.id"
            v-bind:root="true"
            v-on:onDrop="onDrop"
      />
    </ul>
  </div>
</template>

<script>
import node from "@/components/node";

export default {
  components: {node},
  props: ['nodes'],
  data: () => {
    return {
      startDrag: 0,
    }
  },
  methods: {
    onDrop: function (id) {
      console.log('Level 1 StartID: ',this.$root.startID);
      console.log('Level 1 Drop: ',id);
    }
  },
}
</script>

<style scoped>

.treeview {
  padding: 0px;
  width: 25%;
  height: 100%;
  background-color: #eeeeee;
  float: left;
}

.tree-list {
  margin: 0;
  padding: 0;
  user-select: none;
  list-style-type: none;
}

</style>