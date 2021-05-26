<template>
  <v-container>
    <!-- Stack the columns on mobile by making one full-width and the other half-width -->
    <v-row>
      <v-col
        cols="12"
        md="4"
      >
        <v-card
          class="rounded-lg"
          elevation = "5"
          tile
        >
          <v-card-title>Apparence</v-card-title>
          <v-card-subtitle>Personnaliser l'apparence de votre interface</v-card-subtitle>
          <v-card-text>
            <v-switch
              v-model="$vuetify.theme.dark"
              label = "Mode sombre"
              color = "accent"
            ></v-switch>
          </v-card-text>
        </v-card>
      </v-col>
      <v-col
        cols="6"
        md="4"
      >
        <v-card
          class="pa-2"
          elevation = "5"
          tile
        >
          <v-sparkline
            :value="value"
            :gradient="gradient"
            :smooth="radius || false"
            :padding="padding"
            :line-width="width"
            :stroke-linecap="lineCap"
            :gradient-direction="gradientDirection"
            :fill="fill"
            :type="type"
            :auto-line-width="autoLineWidth"
            auto-draw
          ></v-sparkline>
        </v-card>
      </v-col>
    </v-row>

    <!-- Columns start at 50% wide on mobile and bump up to 33.3% wide on desktop -->
    <v-row>
      <v-col
        v-for="n in 3"
        :key="n"
        cols="6"
        md="4"
      >
        <v-card
          class="pa-2"
          elevation = "5"
          tile
        >
          <breeding-rhombus-spinner
              :animation-duration="2000"
              :size="30"
              :color="loadingColor"
          />
          <trinity-rings-spinner
              :animation-duration="1500"
              :size="30"
              :color="loadingColor"
          />
        </v-card>
      </v-col>
    </v-row>

    <!-- Columns are always 50% wide, on mobile and desktop -->
    <v-row>
      <v-col
        v-for="n in 2"
        :key="n"
        cols="6"
      >
        <v-card
          class="pa-2"
          elevation = "5"
          tile
        >
          .col-6
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
  export default {
    name: 'Settings',

    data: () => ({
      width: 2,
      radius: 10,
      padding: 8,
      lineCap: 'round',
      gradient: [this.$vuetify.theme.currentTheme.accent],
      value: [0, 2, 5, 9, 5, 10, 3, 5, 0, 0, 1, 8, 2, 9, 0],
      gradientDirection: 'top',
      fill: false,
      type: 'trend',
      autoLineWidth: false,
    }),

    computed: {
      loadingColor() {
        return this.$vuetify.theme.currentTheme.accent
      }
    },
  }
</script>
