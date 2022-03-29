<template>
  <v-container>
    <v-row no-gutters>
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
            <v-btn color="dark lighten-2" text> Explore </v-btn>

            <v-spacer></v-spacer>

            <v-btn icon @click="show = !show">
              <v-icon>{{
                show ? "mdi-chevron-up" : "mdi-chevron-down"
              }}</v-icon>
            </v-btn>
          </v-card-actions>

          <v-expand-transition>
            <div v-show="show">
              <v-divider></v-divider>

              <v-card-text> {{ film.descrizione }} </v-card-text>
            </div>
          </v-expand-transition>

          <v-img
            height="250"
            :src="`https://image.tmdb.org/t/p/${imageDimension}/${film.image}`"
          ></v-img>

          <v-card-title>{{ film.title }}</v-card-title>

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

          <v-divider class="mx-4"></v-divider>

          <!-- <v-card-actions>
          <v-btn color="deep-purple lighten-2" text @click="reserve">
            Reserve
          </v-btn>
        </v-card-actions> -->
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  name: "mainApp",

  data: () => ({
    show: false,
    imageDimension: ["original"],
    loading: false,
    selection: 1,
  }),
  props: {
    filmList: [Object, Array],
    search: [String],
  },

  methods: {
    reserve() {
      this.loading = true;

      setTimeout(() => (this.loading = false), 2000);
    },
  },
};
</script>
<style lang="scss" scoped>
$card-text: 150px;

.card-text {
  min-height: 150px;
  max-height: 150px;
  overflow-y: scroll;
}
</style>
