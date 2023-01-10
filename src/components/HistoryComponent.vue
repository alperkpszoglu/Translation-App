<template>
  <div class="wrapper">
    <h3>Arama Geçmişi</h3>
    <ul class="list-group text-left" v-for="el in history" :key="el.translateText">
      <li class="list-item-custom mt-3">
        <div>
          <strong>{{ el.from }} <i class="fa-sharp fa-solid fa-arrow-right"></i> {{ el.to }}</strong>
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

<style scoped>
body {
  overflow-y: visible;
}

.list-item-custom {
  border-top: 1px solid rgb(190, 190, 190);
  list-style-type: none;
  padding-top: 0.75rem;
}
.list-group:last-child {
  border-bottom: 1px solid rgb(190, 190, 190);
  border-radius: 0;
  padding-bottom: 0.75rem;
}
</style>
