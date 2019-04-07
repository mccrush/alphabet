<template>
  <nav class="navbar navbar-expand-lg navbar-light bg-white justify-content-between">
    <img src="img/icons/favicon-32x32.png" width="32" height="32" :alt="local.titleapp">
    <span class="font-roboto-slab">{{local.titleapp}}</span>
    <i class="material-icons md-24 btn btn-sm" :title="local.settings" data-toggle="tooltip" data-placement="left" @click="showSettings">settings</i>
  </nav>
</template>
<script>
export default {
  props: {
    local: Object
  },
  methods: {
    showSettings: function() {
      let settings = document.querySelector("#settings");
      if (!this.statusShow) {
        settings.style = "right:0px";
        this.statusShow = true;
      } else {
        settings.style = "right:-260px";
        this.statusShow = false;
      }
    }
  }
};
</script>