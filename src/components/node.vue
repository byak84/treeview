<template>
  <div class="node" draggable="false">

    <!-- TITLE -->
    <table border="0" width="100%">
      <tr>
        <td width="100%">
          <div v-bind:class="{root_title: root, sub_item: !root}">
            <li v-on:click="isNested = !isNested">{{ node.name }}</li>
          </div>
        </td>
        <td v-if="closeable">
          <div>
            <closebtn
                v-on:closeClick="deleteItem"
            />
          </div>
        </td>
      </tr>
    </table>
    <!-- TITLE -->

    <!-- IF NODES EXIST -->
    <div v-if="node.nodes.length !== 0" v-bind:class="{root_body: root}">

      <ul class="sub-tree" v-bind:class="{nested: !isNested, visible: isNested}">

        <div v-for="node in node.nodes" draggable="true" class="subnode"
             v-bind:key="node.id"
        >

          <!--          <table border="1">-->
          <!--            <tr>-->
          <!--              <td width="100%">-->
          <node
              v-bind:node="node"
              v-bind:root="false"
              v-bind:closeable="true"
          />
          <!--              </td>-->
          <!--              <td>-->
          <!--                <closebtn-->
          <!--                    v-on:closeClick="deleteItem"-->
          <!--                />-->
          <!--              </td>-->
          <!--            </tr>-->
          <!--          </table>-->
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
    }
  },
  methods: {
    deleteItem: function (cxt) {
      console.log(this.$props.node.id);
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
  /*margin-bottom: 10px;*/
}


.root_title {
  font-family: Verdana Tahoma Arial;
  font-size: 18px;
  background-color: dodgerblue;
  color: #ffffff;
  text-align: left;
  margin-top: 0px;
  margin-bottom: 10px;
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
  width: 100%;
  background-color: white;
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

.visible {
  transition: all 2s linear;
  display: block;
  color: red;
}

.nested {
  display: none;
  opacity: 0;
}
</style>