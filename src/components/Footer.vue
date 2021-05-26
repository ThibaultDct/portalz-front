<template>
  <!------------ FOOTER ------------>
  <v-footer absolute>
    <v-tooltip v-if="!$vuetify.theme.dark" right>
      <template v-slot:activator="{ on }">
        <v-btn v-on="on" color="accent" small fab @click="darkMode">
          <v-icon class="mr-1">mdi-moon-waxing-crescent</v-icon>
        </v-btn>
      </template>
      <span>Mode Sombre</span>
    </v-tooltip>

    <v-tooltip v-else right>
      <template v-slot:activator="{ on }">
        <v-btn v-on="on" color="accent" small fab @click="darkMode">
          <v-icon color="mr-1">mdi-white-balance-sunny</v-icon>
        </v-btn>
      </template>
      <span>Mode Clair</span>
    </v-tooltip>

    <v-tooltip right v-if="!this.$session.exists()">
      <template v-slot:activator="{ on }">
        <v-btn v-on="on" color="accent" small fab @click="newSession">
          <v-icon class="mr-1">mdi-account-plus</v-icon>
        </v-btn>
      </template>
      <span>Démarrer session</span>
    </v-tooltip>
    <v-spacer></v-spacer>
    <div>&copy; Portalz {{ new Date().getFullYear() }}</div>
  </v-footer>
  <!--------------------------------->
</template>

<script>
export default {
  name: "Footer",

  methods: {
    darkMode() {
      this.$vuetify.theme.dark = !this.$vuetify.theme.dark;
    },
    newSession() {
      this.$session.start();
      this.$router.push("/dashboard")
      this.$router.go()
    },
  },

}

</script>

<style scoped>

</style>