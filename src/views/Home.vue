<template>
  <div class="container mt-4">
    <div style="left: 665px; top: 94px; visibility: visible; " id="workGround">
      <div id="voiceLetter"></div>
      <div id="moveLetter"></div>
    </div>
    <!-- <div class="row justify-content-center">
      <div class="col">
        
      </div>
    </div>-->
  </div>
</template>

<script>
// @ is an alias to /src
//import HelloWorld from '@/components/HelloWorld.vue'

export default {
  name: "home",
  components: {},
  props: {
    local: Object
  },
  data() {
    return {
      alphabet: this.local.alphabet,
      delay: 2000
    };
  },
  created() {
    if (localStorage.getItem("settings")) {
      this.settings = JSON.parse(localStorage.getItem("settings"));
      this.delay = this.settings.delay;
    }
  },
  mounted() {
    this.nextLetter();
  },
  methods: {
    nextLetter() {
      var continium;
      var letterIndex = this.alphabet.length;
      if (letterIndex == this.alphabet.length) {
        continium = this.generateAlphabet();
        letterIndex = 0;
      }
      var wg = document.getElementById("workGround");
      wg.style.visibility = "hidden";
      var dw = document.documentElement.clientWidth;
      var dh = document.documentElement.clientHeight;
      if (dh < 50) dh = document.body.clientHeight;
      wg.style.left = Math.ceil(Math.random() * (dw - 300)) + "px";
      wg.style.top = Math.ceil(Math.random() * (dh - 400)) + 40 + "px";
      document.getElementById("voiceLetter").innerHTML =
        continium[0][letterIndex];
      document.getElementById("moveLetter").innerHTML =
        continium[1][letterIndex];
      wg.style.visibility = "visible";

      letterIndex++;

      setTimeout(this.nextLetter, this.delay);
    },
    generateAlphabet() {
      var LEFT = this.local.simbols.left;
      var RIGHT = this.local.simbols.right;
      var BOTH = this.local.simbols.both;
      var l = this.alphabet.length;
      var moves = new Array(l);
      var coeffs = new Array(l);
      var letters = new Array(l);
      var letterIndeces = new Array(l);

      for (var i = 0; i < l; i++)
        coeffs[(letterIndeces[i] = i)] = Math.random();

      function swap(a, i1, i2) {
        var t = a[i1];
        a[i1] = a[i2];
        a[i2] = t;
      }

      for (var i = l - 1; i > 1; i--)
        for (var j = 0; j < i; j++)
          if (coeffs[j] > coeffs[j + 1]) {
            swap(coeffs, j, j + 1);
            swap(letterIndeces, j, j + 1);
          }

      for (var i = 0; i < l; i++)
        switch ((letters[i] = this.alphabet[letterIndeces[i]])) {
          case BOTH:
            moves[i] = BOTH;
            continue;
          case LEFT:
            moves[i] = RIGHT;
            continue;
          case RIGHT:
            moves[i] = LEFT;
            continue;
        }

      var counts = {};
      counts[LEFT] = counts[RIGHT] = counts[BOTH] = 0;

      for (var i = 0; i < l; i++) {
        if (moves[i]) continue;
        var cand,
          rand = Math.random();
        if (rand < 0.333) cand = LEFT;
        else if (rand < 0.666) cand = BOTH;
        else cand = RIGHT;

        if (
          moves[i - 1] == cand &&
          (moves[i + 1] == cand || moves[i - 2] == cand)
        )
          switch (cand) {
            case BOTH:
              cand = counts[LEFT] > counts[RIGHT] ? RIGHT : LEFT;
              break;
            case LEFT:
              cand = counts[RIGHT] > counts[BOTH] ? BOTH : RIGHT;
              break;
            case RIGHT:
              cand = counts[BOTH] > counts[LEFT] ? LEFT : BOTH;
              break;
          }

        counts[cand] = counts[cand] + 1;
        moves[i] = cand;
      }

      return [letters, moves];
    }
  }
};
</script>
<style scoped>
#workGround {
  position: absolute;
  width: 300px;
  font-family: "Roboto Slab", serif;
  font-weight: 700;
  font-size: 90pt;
  font-weight: bold;
  /* color: #c2c2c2; */
  color: #6c757d !important;
  text-shadow: #ffffff 0px 1px 1px;
}

#workGround div {
  text-align: center;
}
</style>
