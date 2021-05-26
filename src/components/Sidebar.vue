<template>
  <!------------ SIDE MENU ------------>
  <v-navigation-drawer
      v-model="drawer"
      :mini-variant="mini"
      :expand-on-hover="expandOnHover"
      permanent
      class="m-0 p-0"
      absolute
      floating
      color="sidebar"
  >
    <v-list-item class="px-2">
      <v-list-item-avatar class="sidebar-logo">
        <Avatar username="Thibault DOUCET"/>
      </v-list-item-avatar>

      <v-list-item-title>Portalz</v-list-item-title>

    </v-list-item>

    <v-divider></v-divider>

    <v-list dense>
      <v-list-item
          v-for="item in items"
          :key="item.title"
          link
          @click="$router.push({ path: item.route })"
      >
        <v-list-item-icon>
          <v-icon class="mr-1">{{ item.icon }}</v-icon>
        </v-list-item-icon>

        <v-list-item-content>
          <v-list-item-title>{{ item.title }}</v-list-item-title>
        </v-list-item-content>
      </v-list-item>
    </v-list>

    <v-divider></v-divider>

    <v-list dense class="justify-end">
      <v-list-item link @click="logout">
        <v-list-item-icon>
          <v-icon class="mr-1">mdi-logout-variant</v-icon>
        </v-list-item-icon>
        <v-list-item-content>
          <v-list-item-title>Déconnexion</v-list-item-title>
        </v-list-item-content>
      </v-list-item>
    </v-list>
  </v-navigation-drawer>
  <!--------------------------------->
</template>

<script>
import Avatar from 'vue-avatar'

export default {

  name: "Sidebar",

  components: {Avatar},

  data: () => ({
    drawer: true,
    items: [
      { title: "Dashboard", icon: "mdi-home-city", route: "/dashboard" },
      { title: "Profil", icon: "mdi-account", route: "/profile" },
      { title: "Utilisateurs", icon: "mdi-account-group-outline" },
      { title: "Paramètres", icon: "mdi-cog", route: "/settings" },
      { title: "Crypto", icon: "mdi-bitcoin", route: "/crypto" },
    ],
    mini: true,
    expandOnHover: true,
  }),
  methods: {
    logout() {
      this.$session.destroy()
      this.$router.push("/")
      this.$router.go()
    }
  },
};
</script>

<style scoped>

</style>