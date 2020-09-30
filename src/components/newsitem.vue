<template>
  <div class="row" draggable="true" @click="itemclick"
       v-on:dragstart="dragStart"
       v-on:dragover="dragOver"
       v-on:dragenter="dragEnter"
       v-on:dragleave="dragLeave"
       v-on:drop="dragDrop"
       v-bind:class="{overed: isOvered, leaved: !isOvered}"

  >

    <li v-bind:class="{item: !isSelected, itemS: isSelected}">{{ news.name }}</li>
<!--    v-bind:data-category="category"-->
<!--    v-bind:data-uuid="news.uuid"-->

  </div>
</template>

<script>
export default {
  props: ['news', 'category'],
  data: () => {
    return {
      isOvered: false,
      isSelected: false,
      counter: 0,
    }
  },
  methods: {
    itemclick: function (event) {
      this.isSelected = true;
      const path = "/" + this.$props.category + "/" + this.$props.news.uuid;
      this.$emit('itemclick', path, this);
    },
    dragStart: function (evn) {
      this.$emit("dragStart", this)
    },
    dragOver: function (evn) {
      evn.preventDefault();
    },
    dragEnter: function () {
      this.isOvered = true;
      this.counter++;
    },
    dragLeave: function () {
      this.counter--;
      if (this.counter === 0) {
        this.isOvered = false;
      }
    },
    dragDrop: function (evt) {
      this.counter = 0;
      this.isOvered = false;
      this.$emit("dragDrop", this)
    }


  }
}
</script>


<style>

.item {
  color: blue;
  user-select: none;
}

.itemS {
  color: blue;
  font-weight: bold;
}

.row:hover {
  /*text-decoration: underline;*/
  background-color: whitesmoke;
}

.overed {
  background-color: burlywood;
}

.leaved {
  background-color: white;
}

.row {
  cursor: pointer;
  width: 85%;
  /*background-color: beige;*/
  /*border-color: black;*/
  /*border-style: groove;*/
  margin: 5px;
  padding: 5px;
}


</style>