<template>
  <div class="node" draggable="false">

    <!-- TITLE -->
    <table border="0" width="100%">
      <tr>
        <td width="100%">
          <div v-if="!root" v-bind:class="{root_title: root, sub_item: !root}" draggable="true"
               v-on:dragstart="dragStart"
               v-on:dragover="dragOver"
               v-on:drop="dragDrop"
          >
            <li v-on:click="isNested = !isNested" v-bind:class="{selected: isSelected}">{{ node.title }}</li>
          </div>
          <div v-else v-bind:class="{root_title: root, sub_item: !root}" v-on:dragstart="dragStart" draggable="false"
               v-on:dragover="dragOver"
               v-on:drop="dragDrop"
          >
            <li v-on:click="isNested = !isNested" v-bind:class="{selected: isSelected}">{{ node.title }}</li>
          </div>

        </td>
        <td v-if="closeable">
          <div>
            <closebtn v-on:deleteClick="deleteItem"/>
          </div>
        </td>
      </tr>
    </table>
    <!-- TITLE -->

    <!-- IF NODES EXIST -->
    <div v-if="node.nodes.length !== 0" v-bind:class="{root_body: root}">

      <ul class="sub-tree" v-bind:class="{nested: !isNested, visible: isNested}">

        <div v-for="node in node.nodes" draggable="false" class="subnode"
             v-bind:key="node.id"
        >
          <node
              v-bind:node="node"
              v-bind:root="false"
              v-bind:closeable="true"
              v-on:onStart="$emit('onStart', node.id)"

          />
        </div>

      </ul>
    </div>
    <!-- IF NODES EXIST -->

  </div>

</template>

<script>
import closebtn from "@/components/closebtn";

export default {
  name: 'node',
  components: {closebtn},
  props: ['node', 'root', 'closeable'],
  data: () => {
    return {
      isOvered: false,
      isSelected: false,
      isNested: true,
      counter: 0,
      startDrag: 0,
    }
  },
  methods: {
    deleteItem: function () {
      const id = this.$props.node.id;
      this.$parent.node.nodes = this.$parent.node.nodes.filter(function (node) {
        return node.id !== id;
      })
    },
    dragStart: function () {
      this.$root.startID = this.$props.node.id;
      this.$root.parent_startID = this.$parent.$props.node.id;
    },
    dragOver: function (evn) {
      evn.preventDefault();
      // console.log("over: ",this.$props.node.id);
    },
    dragDrop: function () {
      console.log("start: ", this.$root.startID);
      console.log("start parent: ", this.$root.parent_startID);
      console.log("drop: ", this.$props.node.id);
      this.$emit('onDrop', this.$props.node.id);
    }
  }
}
</script>

<style scoped>

.node {
  cursor: pointer;
  margin: 0px;
  padding: 0px;
  position: relative;
  height: 100%;
}


.root_title {
  font-family: Verdana Tahoma Arial;
  font-size: 18px;
  background-color: dodgerblue;
  color: #ffffff;
  text-align: left;
  margin-top: 0px;
  margin-bottom: 5px;
  padding: 10px;
}

.root_body {
  /*background-color: white;*/
  /*border-style: solid;*/
  /*child-align: middle;*/
  margin-bottom: 10px;
  padding-right: 10px;
}

.sub_item {
  width: 100%;
  padding-left: 0px;
  margin: 0px;
  padding: 0px;
  float: left;
}

.subnode {
  padding: 0px;
  margin: 10px;
  width: 95%;
  background-color: white;
}

.subnode:hover {
  background-color: #aaaaaa;

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

.visible {
  transition: all 2s linear;
  display: block;
}

.nested {
  display: none;
  opacity: 0;
}

.selected {
  font-weight: bold;
}
</style>