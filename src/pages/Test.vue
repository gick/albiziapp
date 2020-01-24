<template>
  <v-ons-page>

    <div @mousemove="changeLetter">
    <pre style="white-space:">
    <template v-for="item in getHTML">{{ item }}</template>

    </pre>

    </div>
  </v-ons-page>
</template>

<script>
import { text } from "../store/text";
export default {
  data() {
    return {
      text: text,
      alphabet: [
        "a",
        "b",
        "c",
        "d",
        "e",
        "f",
        "g",
        "h",
        "i",
        "j",
        "k",
        "l",
        "m",
        "n",
        "o",
        "p",
        "q",
        "r",
        "s",
        "t",
        "u",
        "v",
        "w",
        "x",
        "y",
        "z"
      ]
    };
  },
  computed: {
    getHTML() {
      return this.text.split("");
    }
  },
  methods: {
    getRandomPos(elem) {
      return Math.floor(Math.random() * (elem.length + 1));
    },
    setHTML() {},
    setText() {
      getRandomString();
    },
    changeLetter() {
      let toRemove = this.getRandomPos(this.text);
      let replaceBy = this.alphabet[this.getRandomPos(this.alphabet)];

      this.text = this.text.split("");

      this.text.splice(toRemove, 1, replaceBy);
      this.text = this.text.join("");
    },
    train() {
      let x = "e";
      x.join();
      return "ddedde";
    }
  }
};
</script>

<style>
.center {
  position: relative;
  top: 50%;
  left: 50%;
}
.list-item {
  display: inline-block;
  margin-right: 2px;
  width: 10px;
}
.list-enter-active,
.list-leave-active {
  transition: all 1s;
}
.list-enter, .list-leave-to /* .list-leave-active below version 2.1.8 */ {
  opacity: 0;
  transform: translateY(30px);
}
</style>