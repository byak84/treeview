<template>
  <div id="app" class="app">
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

export default {
  name: 'App',
  components: {
    Treeview, Textview
  },

  data: () => {
    return ({
      // myTree: {
      //   "Economy": [
      //     {
      //       "id": 3,
      //       "name": "Economy_news1",
      //       "text": "Economy is Great"
      //     },
      //     {
      //       "id": 4,
      //       "name": "Economy_news2",
      //       "text": "Russia economy is bad"
      //     }
      //   ],
      //   "Politic": [
      //     {
      //       "id": 1,
      //       "name": "Politic_news1",
      //       "text": "Something about Poly"
      //     },
      //     {
      //       "id": 2,
      //       "name": "Politic_news2",
      //       "text": "Poly, poly holy"
      //     }
      //   ]
      // },
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
  padding: 0px;
}

.app {
  height: 100%;
}

</style>
