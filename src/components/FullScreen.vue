<template>
  <div>
    <i class="material-icons md-48 full mr-3 mb-4" :title="local.fullscreen" data-toggle="tooltip" data-placement="left" @click="fullScreen">fullscreen</i>
  </div>
</template>

<script>
export default {
  props: {
    local: Object
  },
  data() {
    return {
      fullscr: false
    };
  },
  methods: {
    fullScreen() {
      if (this.fullscr) {
        this.cancelFullscreen();
        this.fullscr = false;
      } else {
        this.launchFullScreen(document.documentElement);
        this.fullscr = true;
      }
    },
    launchFullScreen(element) {
      if (element.webkitRequestFullScreen) {
        element.webkitRequestFullScreen();
        let navbarTop = document.querySelector("#navbarTop");
        navbarTop.style = "display: none;";
      }
    },
    cancelFullscreen() {
      if (document.webkitCancelFullScreen) {
        document.webkitCancelFullScreen();
        let navbarTop = document.querySelector("#navbarTop");
        navbarTop.style = "display: flex;";
      }
    }
  }
};
</script>
<style scoped>
.full {
  position: fixed;
  bottom: 10px;
  right: 0;
  opacity: 0.3;
  cursor: pointer;
}
</style>
