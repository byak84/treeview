<template>
  <div class="node" draggable="false">

    <!-- TITLE -->
    <div v-bind:class="{root_title: root, sub_item: !root}">
      <li v-on:click="isNested = !isNested">{{ node.name }}</li>
    </div>
    <!-- TITLE -->

    <!-- IF-->
    <div v-if="node.nodes.length !== 0" v-bind:class="{root_body: root}">

      <ul class="sub-tree" v-bind:class="{nested: !isNested}">

        <div v-for="node in node.nodes" draggable="true" class="subnode"
             v-bind:key="node.id">

          <table border="0">
            <tr>
              <td width="100%">
                <node
                    v-bind:node="node"
                    v-bind:root="false"
                />
              </td>
              <td>
                <closebtn />
              </td>
            </tr>
          </table>
        </div>


      </ul>
    </div>
    <!-- IF -->

  </div>

</template>

<script>
import closebtn from "@/components/closebtn";
export default {
  name: 'node',
  components: {closebtn},
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
  position: relative;
  height: 100%;
  margin-bottom: 10px;
}

.root_title {
  font-family: Verdana Tahoma Arial;
  font-size: 18px;
  background-color: dodgerblue;
  color: #ffffff;
  /*min-height: 40px;*/
  text-align: left;
  margin-bottom: 10px;
  padding: 10px;
}

.root_body {
  /*background-color: white;*/
  /*border-style: solid;*/
}

.sub_item {
  /*width: 100%;*/
  vertical-align: center;
  padding-left: 10px;
  height: 100%;
  /*border-style: dashed;*/
  margin: 0px;
  padding: 0px;
}

.subnode {
  margin-right: 50px;
  padding: 5px;
  width: 100%;
}

.subnode:hover {
  background-color: #888888;

}

li {
  margin: 0;
  padding: 0;
}

.sub-tree {
  user-select: none;
  list-style-type: none;
  padding: 0px;
  margin-left: 50px;
}

.nested {
  display: none;
}
</style>