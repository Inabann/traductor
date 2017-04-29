<template>
  <div id="app" class="text-center">
    <h1 >Traductor</h1>
    <h5>Hecho con Vue.js</h5>
    <TranslateForm v-on:formSubmit="translateText"></TranslateForm>
    <TranslateOutput v-text="translatedText"></TranslateOutput>
  </div>
</template>

<script>
import TranslateForm from './Components/TranslateForm'
import TranslateOutput from './Components/TranslateOutput'

export default {
  name: 'app',
  components: {
    TranslateForm,
    TranslateOutput
  },
  data: function(){
    return {
      translatedText:''
    }
  },
  methods: {
    translateText: function(text, language){
      this.$http.get('https://translate.yandex.net/api/v1.5/tr.json/translate?key=trnsl.1.1.20170429T001014Z.5949146c4275f784.bbc29996157c172b2bc7aed67f688798b66342fe&lang='+language+'&text='+text)
      .then((res) => {
        this.translatedText = res.body.text[0];
      });
    }
  }
}
</script>

<style>
body {
  background: #fefefe;
}
</style>
