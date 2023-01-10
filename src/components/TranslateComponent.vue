<template>
  <form class="wrapper" @submit.prevent="OnTranslate">
    <select class="form-control mb-3" v-model="translateTo">
      <option v-for="(value, key) in languages[0]" :value="key" :key="value.name">{{ value.name }}</option>
    </select>
    <textarea
      style="resize: none"
      cols="30"
      rows="5"
      class="form-control"
      placeholder="Çevirmek istediğiniz kelime/cümle yazınız."
      v-model="translateText"
    ></textarea>
    <br />
    <div class="text-left" v-if="translateFrom">
      <strong>Tespit Edilen Dil : {{ this.languages[0][translateFrom].name }} </strong>
    </div>
    <br />
    <button type="submit" class="btn btn-dark float-end"><i class="fa fa-globe" aria-hidden="true"></i> Çevir</button>
  </form>
</template>

<script>
import axios from 'axios';
export default {
  data() {
    return {
      languages: [],
      translateText: '',
      translateFrom: null,
      translateTo: null,
    };
  },
  methods: {
    OnTranslate() {
      //for detected lang
      axios({
        url: 'https://api.cognitive.microsofttranslator.com/detect/',
        method: 'post',
        headers: {
          'Ocp-Apim-Subscription-Key': '3874c4628f4841bd8241136edb5a73bf',
          'Ocp-Apim-Subscription-Region': 'westeurope',
          'Content-Type': 'application/json',
        },
        params: {
          'api-version': '3.0',
        },
        data: [
          {
            text: this.translateText,
          },
        ],
      })
        .then((response) => {
          this.translateFrom = response.data[0].language;
        })
        .then(() => {
          axios({
            url: 'https://api.cognitive.microsofttranslator.com/translate',
            method: 'post',
            headers: {
              'Ocp-Apim-Subscription-Key': '3874c4628f4841bd8241136edb5a73bf',
              'Ocp-Apim-Subscription-Region': 'westeurope',
              'Content-type': 'application/json',
            },
            params: {
              'api-version': '3.0',
              from: this.translateFrom,
              to: [this.translateTo],
            },
            data: [
              {
                text: this.translateText,
              },
            ],
          }).then((res) => {
            let history = {
              translateText: this.translateText,
              translatedText: res.data[0].translations[0].text,
              from: this.languages[0][this.translateFrom].name,
              to: this.languages[0][this.translateTo].name,
            };
            this.$emit('translateTextEvent', res.data[0].translations[0].text);
            this.emitter.emit('sendToHistory', history);
            history = {};
          });
        });
    },
  },
  created() {
    axios.get('https://api.cognitive.microsofttranslator.com/languages?api-version=3.0').then((res) => {
      this.languages.push(res.data.translation);
      this.translateTo = 'en';
    });
  },
};
</script>
