<template>
  <li class="item" @click="itemclick" v-bind:data-category="category" v-bind:data-id="news.id">{{ news.name }}</li>
</template>

<script>
export default {
  props: ['news', 'category'],
  methods: {
    itemclick: function (event) {
      const path = event.target.dataset.category + "/" + event.target.dataset.id;
      this.$emit('itemclick', path);
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

</style>