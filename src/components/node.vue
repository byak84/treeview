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
             v-bind:key="node.id"
        >
          <table border="0">
            <tr style="min-height: 70px">
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
  /*vertical-align: middle;*/
  /*background-color: aqua;*/
  /*border-style: solid;*/
  position: relative;
  height: 100%;
}

.root_title {
  font-family: Verdana Tahoma Arial;
  font-size: 18px;
  background-color: dodgerblue;
  min-height: 40px;
  text-align: left;
  margin: 0px;
  padding: 0px;
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
}

.subnode:hover {
  background-color: #337AB7;
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