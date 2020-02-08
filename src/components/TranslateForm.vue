<template>
  <div>
    <form @submit.prevent="translateIt" class="well">
      <textarea
        v-model="translateText"
        cols="30"
        rows="5"
        class="form-control"
        placeholder="Çevirmek istediğiniz kelime/cümle yazınız."
      ></textarea>
      <select v-model="translateTo" class="form-control">
        <option v-for="(value,key) in langs" :key="key" :value="key">{{value}}</option>
      </select>
      <br />
      <div class="text-left">
        <strong>Tespit Edilen Dil :</strong>
        {{detectedLanguage}}
      </div>
      <br />
      <button type="submit" class="btn btn-primary btn-block">Çevir Gelsin!</button>
    </form>
  </div>
</template>

<script>
import axios from "axios";
import { YANDEX_API_KEY } from "../../private/keys";
export default {
  data() {
    return {
      translateTo: "",
      translateText: "",
      langs: {},
      detectedLanguage: ""
    };
  },
  methods: {
    translateIt() {
      let url = "https://translate.yandex.net/api/v1.5/tr.json/translate";
      axios
        .get(
          url +
            "?key=" +
            YANDEX_API_KEY +
            "&text=" +
            this.translateText +
            "&lang=" +
            this.translateTo
        )
        .then(response => {
          this.detectedLanguage = this.langs[response.data.lang.split("-")[0]];
          this.$emit("result", response.data.text[0]);
          let history = {
              from:this.detectedLanguage,
              to:this.langs[this.translateTo],
              text:this.translateText,
              translatedText:response.data.text[0]
          }
          this.$emit('historyEvent',history)
        })
        .catch(err => console.log(err));
    }
  },
  created() {
    let url = "https://translate.yandex.net/api/v1.5/tr.json/getLangs";
    axios
      .get(url + "?key=" + YANDEX_API_KEY + "&ui=tr")
      .then(response => {
        this.langs = response.data.langs;
      })
      .catch(err => console.log(err));
  }
};
</script>

<style>
</style>