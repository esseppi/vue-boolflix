<template>
  <v-container>
    <v-row no-gutters>
      <v-col v-for="(film, index) in filmList.results" :key="index">
        <v-card :loading="loading" class="mx-auto my-12" max-width="374">
          <template slot="progress">
            <v-progress-linear
              color="deep-purple"
              height="10"
              indeterminate
            ></v-progress-linear>
          </template>

          <v-img
            height="250"
            :src="'https://image.tmdb.org/t/p/original/' + film.backdrop_path"
          ></v-img>

          <v-card-title>{{ film.title }}</v-card-title>

          <v-card-text>
            <v-row align="center" class="mx-0">
              <v-rating
                :value="film.vote_average / 2"
                color="amber"
                dense
                half-increments
                readonly
                size="14"
              ></v-rating>

              <div class="grey--text ms-4">{{ film.vote_average / 2 }}</div>
            </v-row>

            <div class="my-4 text-subtitle-1">{{ film.release_date }}</div>
            <div>{{ film.original_title }}</div>
            <div>{{ film.original_language }}</div>

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
    loading: false,
    selection: 1,
  }),
  props: { filmList: [Object, Array] },

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
  max-height: 150px;
  overflow-y: scroll;
}
</style>
