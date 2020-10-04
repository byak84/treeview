<template>
  <div class="cl-btn-7" v-on:click="closeClick"></div>
</template>

<script>
export default {
  methods: {
    closeClick: function (){
      console.log('close');
    }
  }

}
</script>

<style scoped>
.cl-btn-7 {
  width: 40px;
  height: 40px;
  border-radius: 40px;
  position: relative;
  z-index: 1;
  margin: 20px auto;
  cursor: pointer;
  margin: 0;
  padding: 0;
}
.cl-btn-7:before {
  content: '+';
  color: #337AB7;
  position: absolute;
  z-index: 2;
  transform: rotate(45deg);
  font-size: 50px;
  line-height: 1;
  top: -5px;
  left: 6px;
  transition: all 0.3s cubic-bezier(0.77, 0, 0.2, 0.85);
}
.cl-btn-7:after {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  border-radius: 100%;
  background: #337AB7;
  z-index: 1;
  transition: all 0.3s cubic-bezier(0.77, 0, 0.2, 0.85);
  transform: scale(0.01);
}
.cl-btn-7:hover:after {
  transform: scale(1);
}
.cl-btn-7:hover:before {
  transform: scale(0.8) rotate(45deg);
  color: #fff;
}
</style>