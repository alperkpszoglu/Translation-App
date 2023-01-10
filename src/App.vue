<template>
  <div>
    <div class="section-content">
      <h1 class="section-header"><span class="content-header"> Translate</span> uygulaması</h1>
      <h3>Çevirmek istediğin dili seç ve <b>ÇEVİR</b></h3>
    </div>
    <div class="container">
      <div class="flex-component">
        <div class="col-md-5">
          <Translate @translateTextEvent="translateTextEventHandler" />
        </div>
        <div class="col-md-5">
          <History />
        </div>
      </div>
      <h3 class="text-white text-center mt-5">{{ translateText }}</h3>
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
* {
  box-sizing: border-box;
}
html {
  overflow: scroll;
  overflow-x: hidden;
}
::-webkit-scrollbar {
  width: 0;
  background: transparent;
}
::-webkit-scrollbar-thumb {
  background: #ff0000;
}

body {
  background-color: #ffe53b;
  background-image: linear-gradient(to left, #3a6186, #89253e);
  min-height: 100vh;
  font-family: 'Fira Sans', sans-serif;
  overflow-y: hidden;
}
.flex-component{
  display: flex;
  justify-content: space-around;
}
@media screen and (max-width: 768px) {
  .flex-component{
  display: block;
}
.wrapper{
  margin-top: 3rem;
}
}

.content-header {
  font-family: 'Oleo Script', cursive;
  color: #fcc500;
  font-size: 2.5rem;
}
.section-content {
  text-align: center;
  margin-top: 5rem;
  margin-bottom: 5rem;
}

.wrapper {
  width: 100%;
  max-width: 37.5rem;
  background: #fff;
  box-shadow: 0px 14px 80px rgba(156, 155, 155, 0.4);
  padding: 25px;
  border-radius: 25px;
  height: 400px;
  overflow: auto;
}
</style>
