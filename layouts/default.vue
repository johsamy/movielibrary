<template>
  <v-app dark>
    <v-app-bar fixed app>
      <NuxtLink class="button" :to="{ name: 'index' }">
        <v-img
          :src="require(`~/assets/images/blue_short-tmdb.svg`)"
          max-height="125"
          max-width="230"
          class="ml-6"
        ></v-img>
      </NuxtLink>
    </v-app-bar>
    <v-main>
      <v-container>
        <Nuxt keep-alive/>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
export default {
  name: 'DefaultLayout',
  data() {
    return {
    }
  },
}
</script>
