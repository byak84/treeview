<template>
  <div class="node" draggable="false">

    <div v-bind:class="{root_title: root, sub_item: !root}">
      <li v-on:click="isNested = !isNested">{{ node.name }}</li>
    </div>

    <ul v-if="node.nodes" class="sub-tree" v-bind:class="{nested: !isNested}">

      <div v-bind:class="{root_body: root}"
           v-for="node in node.nodes" draggable="true">

        <node
            v-bind:node="node"
            v-bind:key="node.id"
            v-bind:root="false"
        />

      </div>

    </ul>

  </div>

</template>

<script>
export default {
  name: 'node',
  props: ['node', 'root'],
  data: () => {
    return {
      isOvered: false,
      isSelected: false,
      isNested: true,
      counter: 0,
    }
  },
}
</script>

<style scoped>

.node {
  cursor: pointer;
  margin: 0px;
  padding: 0px;
  /*vertical-align: middle;*/
  background-color: aqua;
  /*border-style: solid;*/
  position: relative;
}

.root_title {
  font-family: Verdana Tahoma Arial;
  font-size: 18px;
  background-color: dodgerblue;
  /*min-height: 40px;*/
  text-align: left;
  margin: 0px;
  padding: 0px;
  /*border-style: dashed;*/
  top: 50%;
}

.root_body {
  /*background-color: white;*/
  border-style: solid;
}

.sub_item {
  /*width: 100%;*/
  min-height: 40px;
  text-align: left;
  vertical-align: center;
  padding-left: 10px;
}

.sub_item:hover {
  background-color: #eeeeee;
}

li {
  margin: 0;
  padding: 0;
}

.sub-tree {
  user-select: none;
  list-style-type: none;
  /*padding: 0;*/
  /*margin: 0;*/
}

.nested {
  display: none;
}
</style>