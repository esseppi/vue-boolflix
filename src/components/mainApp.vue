<template>
  <v-container>
    <v-row> </v-row>
    <v-row v-if="this.filmList.length > 0" no-gutters>
      <v-col
        v-show="film.title && film.image"
        v-for="(film, index) in filmList"
        :key="index"
        cols="3"
      >
        <v-card :loading="loading" class="mx-auto my-12" max-width="374">
          <template slot="progress">
            <v-progress-linear
              color="deep-purple"
              height="10"
              indeterminate
            ></v-progress-linear>
          </template>
          <v-card-actions>
            <v-btn @click="openInfoWindow(index)" color="dark lighten-2" text>
              Info
            </v-btn>

            <v-spacer></v-spacer>

            <v-btn icon @click="openInfoWindow(index)">
              <v-icon>{{
                activeIndex == film.id ? "mdi-chevron-up" : "mdi-chevron-down"
              }}</v-icon>
            </v-btn>
          </v-card-actions>

          <v-expand-transition>
            <div v-show="activeIndex == film.id" slot="back">
              <v-divider></v-divider>

              <v-card-text> {{ film.descrizione }} </v-card-text>
            </div>
          </v-expand-transition>

          <v-img
            height="250"
            :src="`https://image.tmdb.org/t/p/${imageDimension}/${film.image}`"
          ></v-img>

          <v-card-title>{{ film.title }}</v-card-title>
          <v-divider class="mx-4"></v-divider>

          <v-card-text>
            <v-row align="center" class="mx-0">
              <v-rating
                :value="film.voto / 2"
                color="amber"
                dense
                half-increments
                readonly
                size="14"
              ></v-rating>
              <div class="grey--text ms-4">{{ film.voto / 2 }}</div>
            </v-row>
            <div class="my-4 text-subtitle-1">{{ film.dataUscita }}</div>
            <v-row align="center">
              <v-col cols="10">
                <div>{{ film.originalTitle }}</div>
              </v-col>
              <v-col>
                <lang-flag :iso="film.originalLanguage" :squared="false" />
              </v-col>
            </v-row>

            <!-- <div class="card-text">
            {{ film.overview }}
          </div> -->
          </v-card-text>
        </v-card>
      </v-col>
    </v-row>
    <v-row v-else>SCHERMATA DI APERTURA</v-row>
  </v-container>
</template>

<script>
export default {
  name: "mainApp",
  data: () => ({
    activeIndex: "",
    imageDimension: ["original"],
    loading: false,
    selection: 1,
  }),
  props: {
    filmList: [Object, Array],
  },
  methods: {
    openInfoWindow(index) {
      if (this.activeIndex == !this.filmList[index].id) {
        this.activeIndex = this.filmList[index].id;
      } else {
        this.activeIndex = "";
      }
    },
    // effetto card
    reserve() {
      this.loading = true;
      setTimeout(() => (this.loading = false), 2000);
    },
  },
};
</script>
<style lang="scss" scoped>
</style>
