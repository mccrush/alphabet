<template>
  <div id="settings" class="settings shadow bg-white pt-5">
    <form class="mt-3">
      <div class="form-group">
        <label for="selectlanguage">{{local.selectlanguage.title}}</label>
        <select class="form-control form-control-sm" id="selectlanguage" v-model="lang">
          <option>{{local.selectlanguage.en}}</option>
          <option>{{local.selectlanguage.ru}}</option>
        </select>
      </div>

      <div class="form-group">
        <label for="selectdelay">{{local.selectdelay.title}}</label>
        <input class="form-control form-control-sm" type="number" id="selectdelay" min="1000" max="9000" step="500" v-model="delay">
      </div>

      <button class="btn btn-success btn-block btn-sm" @click.prevent="saveSettings">{{local.buttonsave}}</button>
    </form>
    <hr>
    <button class="btn btn-light btn-sm btn-block dropdown-toggle mt-3" type="button" data-toggle="collapse" data-target="#collapseSettings" aria-expanded="false" aria-controls="collapseSettings">{{local.buttonaboutapp}}</button>
    <div v-html="local.descriptionapp" class="mt-3 collapse" id="collapseSettings"></div>
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
      settings: {},
      delay: 2000
    };
  },
  created() {
    if (localStorage.getItem("settings_alphabet")) {
      this.settings = JSON.parse(localStorage.getItem("settings_alphabet"));
      this.lang = this.settings.language;
      this.delay = this.settings.delay;
    } else {
    }
  },
  methods: {
    saveSettings() {
      this.settings.language = this.lang;
      if (this.lang == "En") {
      } else {
      }
      this.settings.delay = this.delay;
      localStorage.setItem("settings_alphabet", JSON.stringify(this.settings));
      location.reload();
    }
  }
};
</script>

<style scoped>
.settings {
  width: 0px;
  height: 100%;
  position: absolute;
  top: 0px;
  right: 0px;
  transition: 0.3s;
  overflow-y: auto;
  overflow-x: hidden;
}
.form-control:focus {
  outline: none;
}
</style>
