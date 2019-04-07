<template>
  <div id="app">
    <Navbar :local="local"/>
    <!-- <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link>
    </div>-->
    <router-view :local="local"/>
    <Footer :local="local"/>

    <Settings :local="local"/>

    <Modal :local="local"/>
    <FullScreen :local="local"/>
  </div>
</template>
<script>
import En from "@/language/en.js";
import Ru from "@/language/ru.js";

import Navbar from "@/components/Navbar.vue";
import Footer from "@/components/Footer.vue";
import Settings from "@/components/Settings.vue";
import Modal from "@/components/Modal.vue";
import FullScreen from "@/components/FullScreen.vue";

export default {
  components: {
    Navbar,
    Footer,
    Settings,
    Modal,
    FullScreen
  },
  data() {
    return {
      local: {}
    };
  },
  created() {
    // Если есть настройки, то берем значение языка
    if (localStorage.getItem("settings_alphabet")) {
      if (
        JSON.parse(localStorage.getItem("settings_alphabet")).language == "Ru"
      ) {
        this.local = Ru;
      } else {
        this.local = En;
      }
    } else {
      this.local = En;
    }

    $(function() {
      $('[data-toggle="tooltip"]').tooltip();
      if (
        !localStorage.getItem("showmodal_alphabet") ||
        localStorage.getItem("showmodal_alphabet") == true
      ) {
        $("#modalWindow").modal("show");
      }
    });
  }
};
</script>

<style scoped>
</style>
