<template>
  <div>
    <div class="caption" v-on:dragover="dragOver" v-on:drop="drop">
      <li class="caret" v-on:click="nes = !nes"
          v-bind:class="{caretdown: !nes}">{{ title }}
      </li>
    </div>
    <ul v-bind:class="{nested: nes}">
      <newsitem
          v-for="(news,index) of newsArray"
          v-bind:news="news"
          v-bind:key="index"
          v-bind:category="title"
          v-on:itemclick="itemclick"
          v-on:dragStart="dragStart"
          v-on:dragDrop="dragDrop"
          v-on:deleteItem="deleteItem"
      />
    </ul>
  </div>
</template>

<script>
import Newsitem from "@/components/newsitem";

export default {
  components: {Newsitem},
  props: ['title', 'newsArray'],

  data: () => {
    return ({
      nes: false,
      startUUID: null
    })
  },
  methods: {
    unselectAll: function (contex) {
      let children = this.$children;
      children.forEach(function (item, i, children) {
        if (item != contex) {
          item.isSelected = false;
        }
      })
    },
    itemclick: function (path, contex) {
      this.$emit("itemclick", path, contex);
    },
    dragOver: function (evn) {
      evn.preventDefault();
    },
    dragStart: function (uuid) {
      this.startUUID = uuid;
      console.log("start: ", uuid);
    },
    dragDrop: function (uuid) {
      console.log("drop:  ", uuid);

      // const tmpD = Object.assign({}, contex.$props.news);
      // const tmpS = Object.assign({}, this.startItem.$props.news);
      // this.startItem.$props.news.uuid = "";
      // contex.$props.news.uuid = tmpS.uuid;
      // contex.$props.news.name = tmpS.name;
      // contex.$props.news.order = tmpS.order;
      // contex.$props.news.text = tmpS.text;
      // this.startItem.$props.news.uuid = tmpD.uuid;
      // this.startItem.$props.news.name = tmpD.name;
      // this.startItem.$props.news.order = tmpD.order;
      // this.startItem.$props.news.text = tmpD.text;

      // }
    },
    deleteItem: function (uuid, cat) {
      this.$emit("deleteItem", uuid, cat);
    },
    drop: function () {
      console.log("dropping... ", this.title);
    }
  }
}

</script>

<style \scoped>

ul {
  list-style-type: none;
}

.caret {
  cursor: pointer;
  user-select: none;
  list-style-type: none;
}

.caret::before {
  content: "\00BB";
  color: black;
  display: inline-block;
  margin-right: 6px;
}

.caretdown::before {
  transform: rotate(90deg);
}

.nested {
  display: none;
}

.active {
  display: block;
}

.caption {
  font-family: Consolas;
  font-size: 19px;
  font-weight: bold;
  background-color: #337AB7;
  color: white;
  width: 80%;
  height: 20px;
  padding: 8px;
  margin-left: 10px;
  margin-bottom: 3px;
}

</style>
