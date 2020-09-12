<template>
  <div id="app" class="app">
    <tophead />
    <treeview v-bind:tree="this['myTree']"
              v-on:itemclick="itemclick"
    />
    <textview v-bind:text="this['text']"
    />
  </div>
</template>

<script>
import Treeview from "@/components/treeview"
import Textview from "@/components/textview"
import Tophead from "@/components/tophead"

export default {
  name: 'App',
  components: {
    Treeview, Textview, Tophead,
  },

  data: () => {
    return ({
      myTree: {},
      text: "",
      apiURL: "http://192.168.2.65:5000/",
    });
  },
  methods: {
    itemclick: function (path) {
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
    }
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
  height: 90%;
  padding: 0;
}

.app {
  height: 100%;
}

</style>
