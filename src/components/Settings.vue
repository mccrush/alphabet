<template>
  <div id="settings" class="settings shadow bg-white pt-5 pl-3 pr-3">
    <form class="mt-3">
      <div class="form-group">
        <label for="selectlanguage">{{local.selectlanguage.title}}</label>
        <select class="form-control form-control-sm" id="selectlanguage" v-model="lang">
          <option>{{local.selectlanguage.en}}</option>
          <option>{{local.selectlanguage.ru}}</option>
        </select>
      </div>

      <!-- <div class="form-group">
        <label for="selectshowtime">{{local.selectshowtime.title}}</label>
        <select class="form-control form-control-sm" id="selectshowtime" v-model="showtime">
          <option>{{local.selectshowtime.yes}}</option>
          <option>{{local.selectshowtime.no}}</option>
        </select>
      </div>-->
      <button class="btn btn-success btn-block btn-sm" @click.prevent="saveSettings">{{local.buttonsave}}</button>
    </form>
    <div v-html="local.descriptionapp" class="mt-2"></div>
  </div>
</template>

<script>
export default {
  props: {
    local: Object
  },
  data() {
    return {
      lang: "En",
      settings: {}
    };
  },
  created() {
    if (localStorage.getItem("settings")) {
      this.settings = JSON.parse(localStorage.getItem("settings"));
      this.lang = this.settings.language;
    } else {
    }
  },
  methods: {
    saveSettings() {
      this.settings.language = this.lang;
      if (this.lang == "En") {
      } else {
      }

      localStorage.setItem("settings", JSON.stringify(this.settings));
      location.reload();
    }
  }
};
</script>

<style scoped>
.settings {
  width: 250px;
  height: 100%;
  position: absolute;
  top: 0px;
  right: -260px;
  transition: 0.3s;
}
.form-control:focus {
  outline: none;
}
</style>
