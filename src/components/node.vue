<template>
  <div class="node" draggable="true">
    <table border="1" width="90%">
      <tr>
        <td>
          <div v-bind:class="{root: root}"><li v-on:click="isNested = !isNested">{{ node.name }}</li></div>
          <ul v-if="node.nodes" class="sub-tree" v-bind:class="{nested: !isNested}">
            <node v-for="node in node.nodes"
                  v-bind:node="node"
                  v-bind:root="false"
            />
          </ul>
        </td>
      </tr>
    </table>
  </div>
</template>

<script>
export default {
  name: 'node',
  props: ['node','root'],
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
  width: 85%;
  /*background-color: beige;*/
  /*border-color: black;*/
  /*border-style: groove;*/
  margin: 5px;
  padding: 5px;
}

.root {
  background-color: beige;
  /*border-color: black;*/
  /*border-style: groove;*/
  width: 100%;
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