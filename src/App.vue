<template>
  <div id="app" class="app">
<!--    <action v-on:add_news="add_news"-->
<!--    />-->

    <treeview v-bind:nodes="treeJSON"
    />


  </div>
</template>

<script>
import Treeview from "@/components/treeview"
import Action from "@/components/action"
import json from './menu.json'
export default {
  name: 'App',
  components: {
    Treeview, Action,
  },

  data: () => {
    return ({
      treeJSON: {},
    });
  },
  methods: {
    itemclick: function (path) {
      // this.currentCategory = path.substr(1).split("/", 1).toString();
      // fetch(this.apiURL + path)
      //     .then(response => {
      //       response.json()
      //           .then(data => {
      //             this.text = data.text;
      //           })
      //     })
      //     .catch(err => {
      //       alert(err);
      //     })
    },
    add_news: function (link) {
      // console.log(link);
      // let post_options = {
      //   link: link
      // }
      // fetch(this.apiURL + "/add/" + this.currentCategory + "/", {
      //   method: 'POST',
      //   headers: {
      //     'Accept': 'application/json',
      //     'Content-Type': 'application/json'
      //   },
      //   body: JSON.stringify(post_options)
      // }).then(res => {
      //   // console.log(res)
      // }).catch(err => {
      //   // console.log(err)
      // })
    },
    deleteItem: function (uuid, cat) {
      // console.log("deleteItem: ", uuid);
      //
      // this.myTree[cat] = this.myTree[cat]
      //     .filter(t => {
      //       return t.uuid != uuid;
      //     })
    },
    loadTree: function () {
      this.treeJSON = json;
    },

  },
  created() {
    this.loadTree();
  }
}

</script>

<style>
html, body {
  height: 98%;
  padding: 0;
}

.app {
  height: 98%;
  /*background: cornflowerblue;*/
}

</style>
