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
      nes: true
    })
  },
  methods: {
    itemclick: function (path) {
      this.$emit("itemclick", path);
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
