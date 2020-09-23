<template>
  <div>
    <li class="caret" v-on:click="nes = !nes"
        v-bind:class="{caretdown: !nes}">{{ title }}
    </li>
    <ul v-bind:class="{nested: nes}">

      <newsitem
          v-for="news of newsArray"
          v-bind:news="news"
          v-bind:key="news.id"
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
      nes: true,
      startItem: null
    })
  },
  methods: {
    itemclick: function (path) {
      this.$emit("itemclick", path);
    },
    dragStart: function (contex) {
      console.log("start: ", contex);
      this.startItem = contex;
    },
    dragDrop: function (contex) {
      console.log("Drop: ", contex);
      if (this.startItem != null) {
        const tmpD = Object.assign({}, contex.$props.news);
        const tmpS = Object.assign({}, this.startItem.$props.news);

        this.startItem.$props.news.id = "";


        contex.$props.news.id=tmpS.id;
        contex.$props.news.name = tmpS.name;
        contex.$props.news.order = tmpS.order;
        contex.$props.news.text = tmpS.text;

        this.startItem.$props.news.id = tmpD.id;
        this.startItem.$props.news.name = tmpD.name;
        this.startItem.$props.news.order = tmpD.order;
        this.startItem.$props.news.text = tmpD.text;

        // b = [a, a = b][0];

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
