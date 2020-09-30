<template>
  <div>
    <li class="caret" v-on:click="nes = !nes"
        v-bind:class="{caretdown: !nes}">{{ title }}
    </li>
    <ul v-bind:class="{nested: nes}">
      <newsitem
          v-for="news of newsArray"
          v-bind:news="news"
          v-bind:key="news.uuid"
          v-bind:category="title"
          v-on:itemclick="itemclick"
          v-on:dragStart="dragStart"
          v-on:dragDrop="dragDrop"
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
      startItem: null
    })
  },
  methods: {
    unselectAll: function (contex) {
      // console.log(this);
      let children = this.$children;
      children.forEach(function (item, i, children) {
        if (item != contex) {
          item.isSelected = false;
        }
      })
    },
    itemclick: function (path, contex) {
      this.$emit("itemclick", path, contex);
      let children = this.$children;
      children.forEach(function (item, i, children) {
        console.log(item.$props.news.uuid);
      })
    },
    dragStart: function (contex) {
      this.startItem = contex;
    },
    dragDrop: function (contex) {
      let dropIndex;
      let startIndex;
      if (this.startItem != null) {

        let items = this.$children;
        for (let i = 0; i < items.length; i++) {
          if (items[i] === contex) {
            console.log(i);
            dropIndex = i;
          }
          if (items[i] === this.startItem) {
            console.log(i);
            startIndex = i;
          }
        }

       items[dropIndex].$props.news.name = items[startIndex].$props.news.name;


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

      }
    }
  }
}

</script>

<style scoped>

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
