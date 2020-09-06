<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
    <button v-on:click="getPdf">НАЖМИ ЧТОБЫ ПОЛУЧИТЬ PDF</button>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import jsPDF from 'jspdf'
import myFont from './assets/OpenSans.js'

    
export default {
  name: 'App',
  components: {
    HelloWorld
  },
  beforeCreate(){
    var callAddFont = function () {
    this.addFileToVFS('opensans-normal.ttf', myFont.openSans);
    this.addFont('opensans-normal.ttf', 'myFont', 'normal');
    };
    jsPDF.API.events.push(['addFonts', callAddFont])
  },
  methods: {
    getPdf(){
      
    var doc = new jsPDF();
    var lang = 'ru';
    doc.setLanguage(lang);
    doc.setFont('myFont');
    doc.text('У меня получилась эта дрочь', 10, 10)
    doc.save('checkRu.pdf')

    }
  },
}


</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
