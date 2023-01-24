<template>
  <v-app dark>
    <div v-if="error.statusCode === 404">
      <v-row
        class="my-8"
        justify="center"
        no-gutters
      >
        <v-col lg="2">
            <v-img
              :src="require(`~/assets/images/404-error.svg`)"
              class="ma-8"
            ></v-img>
          <ErrorAlert>{{ pageNotFound }}</ErrorAlert>
        </v-col>
      </v-row>
    </div>
    <div v-else>
      <ErrorAlert>{{ otherError}}</ErrorAlert>
    </div>
    <v-row
      class="my-8"
      justify="center"
      no-gutters
    >
      <NuxtLink to="/">
        <ButtonText>
          Accueil
        </ButtonText>
      </NuxtLink>
    </v-row>
  </v-app>
</template>

<script>
export default {
  name: 'EmptyLayout',
  layout: 'empty',
  props: {
    error: {
      type: Object,
      default: null,
    },
  },
  data() {
    return {
      pageNotFound: '404 Page introuvable',
      otherError: 'Veuillez rafraichir la page ou réessayer plus tard.',
    }
  },
  head() {
    const title =
      this.error.statusCode === 404 ? this.pageNotFound : "Erreur"
    return {
      title,
    }
  },
}

</script>

<style lang="scss" scoped>
</style>
