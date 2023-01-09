<template>
  <div class="history">
    <h3>Arama Geçmişi</h3>
    <ul class="list-group text-left" v-for="el in history" :key="el.translateText">
      <li class="list-group-item">
        <div>
          <strong>{{ el.from }} => {{ el.to }}</strong>
        </div>
        <br />
        <div>
          <strong class="text-success">{{ el.translateText }}</strong>
          <br />
          <span class="text-info">{{ el.translatedText }}</span>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      history: [],
    };
  },
  created() {
    this.emitter.on('sendToHistory', (el) => {
      this.history.unshift(el);
    });
  },
};
</script>

<style></style>
