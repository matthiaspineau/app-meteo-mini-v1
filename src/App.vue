<template>
  <div id="app">
    <!-- Navbar -->
    <nav class="navbar">
      <h1>Méteo</h1>
      <!-- <span>{{ selectLang }}</span> -->
      <div class="wrapper__lang">
        <select v-model="selectLang">
          <option value="fr">Fr</option>
          <option value="en">En</option>
        </select>
      </div>
    </nav>


    <!-- Formulaire -->
    <div class="wrapper__form">
      <div class="form">
        <input :class="errorCity ? 'error' : '' " type="text" v-model.trim="city" :placeholder="lang.form.placeholder" />
        <span v-if="errorCity" class="error__text">{{ lang.form.errorText }}</span>
      </div>
      <div>
        <button class="btn__call" @click="callApi">{{ lang.form.btnSearch }}</button>
      </div>
    </div>

    <!-- Section mid -->
    <section class="section section__mid">
      <!-- Affichage Titre -->
      <Title :file="file"></Title>

      <!-- Table -->
      <Table :file="file" :lang="lang.table"></Table>

    </section>

    <!-- Section bot -->
    <section class="section section__bot">
      
      <Sun :file="file" :lang="lang.sun"></Sun>

    </section>

    <div v-if="loaderVisible" class="wrapper__loader">
      <div class="loader">
        <h3>{{ lang.load }}</h3>
      </div>
    </div>
    <!-- Zone debug
    <div class="debug">
      {{ fileApi }}
    </div> -->
  </div>
</template>

<script>
// import Home from './components/Home.vue'
import example from "./assets/data-test.json";
import Table from "@/components/table/Table.vue";
import Title from "@/components/title/Title.vue";
import Sun from "@/components/sun/Sun.vue";
import Axios from "axios";
import langFr from "@/assets/lang/fr.json";
import langEn from "@/assets/lang/en.json";

const ApiKey = '728e0adecbfd917c5d6a91e18904d29b'
// const units = 'metric'
// const lang = 'fr'

export default {
  name: "App",
  data() {
    return {
      fileExample: example,
      fileApi: null,
      city: "",
      errorCity: false,
      selectLang: 'fr',
      loaderVisible: false
    };
  },
  computed: {
    lang() {
      this.showLoader()
      this.loader()
      return this.selectLang == 'fr' ? langFr.lang : langEn.lang
    },
    file() {
      return this.fileApi != null ? this.fileApi : example;
    },
  },
  methods: {
    callApi: function () {

      this.showLoader()

      this.city = this.city.replace(/ /g,'-').toLowerCase()
      Axios.get("https://api.openweathermap.org/data/2.5/weather?q="+this.city+"&units=metric&lang=fr&appid="+ApiKey)
        .then((response) => {
          this.fileApi = response.data
          this.errorCity = false
          console.log(response.status)
          this.loader()
        })
        .catch((error) => {
          console.log(error.response);
          this.errorCity = true
          this.loader()
        })
    },
    cons() {
      console.log('test')
    },
    showLoader() {
      this.loaderVisible = true;
    },
    hideLoader() {
      this.loaderVisible = false;
    },
    loader() {
      window.setTimeout(this.hideLoader, 1000);
    },
    // clearLoader() {

    // }
  },
    filters: {
    toKm: function (value) {
      return value / 1000
    },
    toDate: function (timeStamp) {
      // var timeStamp = 1345902217, // le TimeStamp à convertir
      let date = new Date(timeStamp * 1000); // pour obtenir le timeStamp en millisecondes

      // let annee = date.getFullYear(); // on récupère l'année
      // let jour = date.getDate(); // on récupère le jour
      // let mois = date.getMonth(); // on récupère le nombre du mois (entre 0 et 11)
      let heure = date.getHours(); // on récupère l'heure
      let min = date.getMinutes(); // on récupère les minutes
      // let sec = date.getSeconds(); // on récupère les secondes
     
      // result = "le "+jour+"/"+mois+"/"+annee+" - "+heure+"h "+min+"min "+sec+"s"
      // console.log(result); // affichera : le 25/08/2012 - 15h 43min 37s
      return heure + ":" + min;
    },
  },
  components: {
    Table,
    Title,
    Sun
  },
};
</script>

<style src="@/assets/scss/app.scss" lang="scss"></style>
