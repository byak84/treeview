<template>
  <div>
    <li class="caret" v-on:click="nes = !nes"
        v-bind:class="{caretdown: !nes}">{{ title }}
    </li>
    <ul v-bind:class="{nested: nes}">
      <template v-if="newsArray.length != 0">
        <newsitem
            v-for="(news,index) of newsArray"
            v-bind:news="news"
            v-bind:key="index"
            v-bind:category="title"
            v-bind:draged="true"
            v-on:itemclick="itemclick"
            v-on:dragStart="dragStart"
            v-on:dragDrop="dragDrop"
            v-on:deleteItem="deleteItem"
        />
      </template>
      <newsitem v-else
                v-bind:news="empty"
                v-bind:draged="false"
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
      startUUID: null,
      empty: {
        "name": "Категория пуста",
        "order": 0,
        "text": "",
        "uuid": "0"
      }
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
  },
  created() {
    // console.log(this.$props.newsArray);
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


</style>
