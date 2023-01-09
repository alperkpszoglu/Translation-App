<template>
  <div class="container">
    <h1 class="text-center">Vue Translator</h1>
    <h5 class="text-center">Vue.js ile Translator</h5>
    <br />
    <div class="row">
      <div class="col-md-12 text-center">
        <Translate @translateTextEvent="translateTextEventHandler" />
        <h3 class="text-success text-center">{{ translateText }}</h3>
        <History />
      </div>
    </div>
  </div>
</template>

<script>
import History from './components/HistoryComponent.vue';
import Translate from './components/TranslateComponent.vue';
export default {
  components: {
    History,
    Translate,
  },
  data() {
    return {
      translateText: '',
    };
  },
  methods: {
    translateTextEventHandler(_translateText) {
      this.translateText = _translateText;
    },
  },
};
</script>

<style>
body {
  background-color: rgb(216, 216, 216);
}
</style>
