<template>
  <div id="app" class="app">
    <action v-on:add_news="add_news"
    />

    <treeview v-bind:tree="this['myTree']"
              v-on:itemclick="itemclick"
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
