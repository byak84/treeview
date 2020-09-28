<template>
  <div class="row" draggable="true" @click="itemclick"
       v-on:dragstart="dragStart"
       v-on:dragover="dragOver"
       v-on:dragenter="dragEnter"
       v-on:dragleave="dragLeave"
       v-on:drop="dragDrop"
       v-bind:class="{overed: isOvered, leaved: !isOvered}"
       v-bind:data-category="category"
       v-bind:data-id="news.id"

  >

    <li class="item"


    >{{ news.name }}</li>


  </div>
</template>

<script>
export default {
  props: ['news', 'category'],
  data: () => {
    return {
      isOvered: false,
      counter: 0,
    }
  },
  methods: {
    itemclick: function (event) {
      // console.log(this);
      // const path = "/" + event.target.dataset.category + "/" + event.target.dataset.id;
      const path = "/" + this.$props.category + "/" + this.$props.news.id;
     // console.log(path);
     this.$emit('itemclick', path);
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
      // console.log("Leaving")
    },
    dragDrop: function (evt) {
      //console.log(this.news);
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

.row:hover {
  /*text-decoration: underline;*/
  background-color: whitesmoke;
}

.overed {
  background-color: deeppink;

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