<template>
  <div class="header">
    <form @submit.prevent="onSubmit">
      <label for="link">Адрес:</label>
      <input class="editlink" type="text" v-model="link" id="link"/>
      <button type="submit">Добавить</button>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      link: ""
    }
  },
  methods: {
    onSubmit: function () {
      if (this.link.trim()) {
        this.$emit('add_news', this.link);
        this.link = "";
      }
    }
  }
}
</script>


<style scoped>

.header {
  width: 100%;
  background-color: cornflowerblue;
  margin: 0;
  padding: 0;
}

.editlink {
  width: 500px;
}

</style>