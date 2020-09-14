<template>
  <div id="app" class="app">
    <tophead v-on:showmodal="showmodal" />
    <treeview v-bind:tree="this['myTree']"
              v-on:itemclick="itemclick"
    />
    <textview v-bind:text="this['text']" />
    <addform v-bind:show="this.modal" />
  </div>
</template>

<script>
import Treeview from "@/components/treeview"
import Textview from "@/components/textview"
import Tophead from "@/components/tophead"
import Addform from "@/components/addform"

export default {
  name: 'App',
  components: {
    Treeview, Textview, Tophead, Addform,
  },

  data: () => {
    return ({
      myTree: {},
      text: "",
      apiURL: "http://192.168.2.65:5000/",
      modal: false,
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
    },
    showmodal: function () {
      //console.log(this.modal);
      this.modal = !this.modal;
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
  height: 90%;
  padding: 0;
}

.app {
  height: 100%;
}

</style>
