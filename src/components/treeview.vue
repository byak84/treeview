<template>
<div class="treeview">

</div>
</template>

<script>
import Category from "@/components/category";

export default {
  components: {Category},
  props: ['tree'],
  methods: {

  }
}
</script>

<style scoped>

.treeview {
  padding: 0px;
  width: 30%;
  height: 100%;
  background-color: #aaaaaa;
  float: left;
}


</style>