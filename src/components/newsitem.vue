<template>
  <li class="item" @click="itemclick" draggable="true"
      v-bind:data-category="category"
      v-bind:data-id="news.id"
      v-on:dragstart="dragStart"
      v-on:dragover="dragOver"
      v-on:dragenter="dragEnter"
      v-on:dragleave="dragLeave"
      v-on:drop="dragDrop"
      v-bind:class="{overed: isOvered}">{{ news.name }}
  </li>
</template>

<script>
export default {
  props: ['news', 'category'],
  data: () => {
    return {
      isOvered: false,
    }
  },
  methods: {
    itemclick: function (event) {
      const path = event.target.dataset.category + "/" + event.target.dataset.id;
      this.$emit('itemclick', path);
    },
    dragStart:function (evn) {
      console.log(this.news);
    },
    dragOver: function (evn) {
      evn.preventDefault();
    },
    dragEnter: function () {
      this.isOvered = true;
    },
    dragLeave: function () {
      this.isOvered = false;
    },
    dragDrop: function (evt) {
      console.log(this.news);
      this.isOvered = false;
    }


  }
}
</script>


<style>

.item {
  cursor: pointer;
  color: blue;
  user-select: none;
}

.item:hover {
  text-decoration: underline;
}

.overed {
  background-color: cornflowerblue;
}

</style>