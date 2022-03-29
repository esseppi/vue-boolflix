<template>
  <v-app>
    <v-app-bar app color="dark" dark>
      <div class="d-flex align-center">
        <v-img
          alt="Vuetify Logo"
          class="shrink mr-2 hidden-md-and-up"
          contain
          src="https://1000logos.net/wp-content/uploads/2017/05/Netflix-Logo-2006.png"
          transition="scale-transition"
          width="40"
        />

        <v-img
          alt="Vuetify Name"
          class="shrink mt-1 hidden-sm-and-down"
          contain
          min-width="100"
          src="https://external-content.duckduckgo.com/iu/?u=http%3A%2F%2F1000logos.net%2Fwp-content%2Fuploads%2F2017%2F05%2FNetflix-Logo.png&f=1&nofb=1"
          width="100"
        />
      </div>

      <v-spacer></v-spacer>
      <v-text-field
        rounded
        single-line
        clearable
        class="shrink"
        hide-details="true"
        flat
        label="Cerca brano"
        dense
        @keyup.enter="changeSearch"
        v-model="searchContent"
      >
      </v-text-field>
      <v-btn @click="changeSearch"><v-icon>mdi-magnify</v-icon></v-btn>
      <v-btn @click="deleteSearch"><v-icon>mdi-delete</v-icon></v-btn>
    </v-app-bar>

    <v-main>
      <mainApp :filmList="filmList" :search="filmList" />
    </v-main>
  </v-app>
</template>

<script>
import mainApp from "./components/mainApp";

export default {
  name: "App",
  data: () => ({
    languageChoosed: ["en-US"],
    myApiKey: "45a3f8865d6c27b9205f8865b3c94dfe",
    filmList: [],
    searchContent: "",
    //
  }),

  components: {
    mainApp,
  },
  methods: {
    changeSearch() {
      const axios = require("axios");
      axios
        .get(
          `https://api.themoviedb.org/3/search/multi?api_key=${this.myApiKey}&language=${this.languageChoosed}&query=${this.searchContent}&include_adult=false`
        )
        .then((response) => {
          this.filmList = response.data.results.map((film) => ({
            title: film.title,
            descrizione: film.overview,
            originalTitle: film.original_title,
            originalLanguage: film.original_language,
            dataUscita: film.release_date,
            voto: film.vote_average,
            image: film.backdrop_path,
          }));
          // handle success
          console.log(this.filmList);
        })
        .catch(function (error) {
          // handle error
          console.log(error);
        });
    },
    deleteSearch() {
      this.searchContent = "";
      this.filmList = [];
    },
  },
  computed: {},
};
</script>
