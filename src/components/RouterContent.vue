<template>
  <!------------ CONTENT ------------>
  <v-content>
    <v-container class='m-2'>
      <v-row class="fill-height">
        <v-col>
          <transition name="fade">
            <router-view></router-view>
          </transition>
        </v-col>
      </v-row>
    </v-container>
  </v-content>
  <!--------------------------------->
</template>

<script>
export default {
  name: "RouterContent"
}
</script>

<style scoped>

</style>