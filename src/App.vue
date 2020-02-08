<template>
  <div>
    <div class="container">
      <h1 class="text-center">Vue-Translator</h1>
      <h5 class="text-center">Vue.js ile Translator</h5>
      <br />
      <div class="row">
        <div class="col-md-12 text-center">
          <app-translate-form
            class="shadow"
            @result="translatedText=$event"
            @historyEvent="history.push($event)"
          ></app-translate-form>
          <h3 v-show="translatedText!=''" class="text-success text-center">{{translatedText}}</h3>
          <app-search-history class="shadow" :history="history"></app-search-history>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import SearchHistory from "./components/SearchHistory";
import TranslateForm from "./components/TranslateForm";
export default {
  components: {
    appSearchHistory: SearchHistory,
    appTranslateForm: TranslateForm
  },
  data() {
    return {
      translatedText: "",
      history: []
    };
  }
};
</script>

<style>
.fade-enter-active,
.fade-leave-active {
  transition: 2s;
}
.fade-enter,
.fade-leave-to {
  height: 0%;
}
</style>
