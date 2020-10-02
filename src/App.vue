<template>
  <div id="app" class="app">
    <action v-on:add_news="add_news"
    />

    <treeview v-bind:tree="this['myTree']"
              v-on:itemclick="itemclick"
              v-on:deleteItem="deleteItem"
    />

    <textview v-bind:text="this['text']"/>
  </div>
</template>

<script>
import Treeview from "@/components/treeview"
import Textview from "@/components/textview"
import Action from "@/components/action"

export default {
  name: 'App',
  components: {
    Treeview, Textview, Action,
  },

  data: () => {
    return ({
      apiURL: "http://192.168.2.65:5000",
      myTree: {},
      text: "",
      currentCategory: "",
    });
  },
  methods: {
    itemclick: function (path) {
      // console.log(path);
      this.currentCategory = path.substr(1).split("/", 1).toString();

      fetch(this.apiURL + path)
          .then(response => {
            response.json()
                .then(data => {
                  this.text = data.text;
                })
          })
          .catch(err => {
            alert(err);
          })
    },
    add_news: function (link) {
      console.log(link);
      let post_options = {
        link: link
      }
      fetch(this.apiURL + "/add/" + this.currentCategory + "/", {
        method: 'POST',
        headers: {
          'Accept': 'application/json',
          'Content-Type': 'application/json'
        },
        body: JSON.stringify(post_options)
      }).then(res => {
        // console.log(res)
      }).catch(err => {
        // console.log(err)
      })
    },
    deleteItem: function (uuid, cat) {
      console.log("deleteItem: ", uuid);
      // let newsArr = this.myTree[cat];

      this.myTree[cat] = this.myTree[cat].filter(function (t) {
        return t.uuid != uuid;
      })
      console.log(this.myTree);
       // newsArr=[];
    },

  },
  mounted() {
    fetch(this.apiURL)
        .then(response => {
          response.json()
              .then(data => {
                this.myTree = data;
              })
        })
        .catch(err => {
          alert(err);
        })

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
