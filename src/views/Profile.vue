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
          <v-card-title>
            <Avatar
                username="Thibault DOUCET"
                class="mr-2"/>
             Thibault DOUCET
          </v-card-title>
          <v-card-subtitle>Visualiser et modifier son profil</v-card-subtitle>
          <!-- POPUP MODIFICATION PROFIL -->
          <v-dialog
              transition="dialog-top-transition"
              max-width="600"
          >
            <template v-slot:activator="{ on, attrs }">
              <v-btn
                  color="accent"
                  v-bind="attrs"
                  v-on="on"
                  class="ml-4"
              >Modifier</v-btn>
            </template>
            <template v-slot:default="dialog">
              <v-card>
                <v-snackbar
                    v-model="snackbar"
                    absolute
                    top
                    right
                    color="success"
                    timeout="2000"
                >
                  <span>Profil modifié avec succès</span>
                  <v-icon dark>
                    mdi-checkbox-marked-circle
                  </v-icon>
                </v-snackbar>
                <v-toolbar
                    color="accent"
                    dark
                >Modifier mon profil</v-toolbar>
                <v-card-text class="pt-3">
                  <v-form
                      ref="form"
                      @submit.prevent="submit"

                  >
                    <Avatar
                        username="Thibault DOUCET"
                        class="mr-2"
                        size="100"
                        inline/> Modifier mon image de profil
                    <v-text-field
                        v-model="form.first"
                        :rules="rules.firstname"
                        color="accent"
                        label="Prénom"
                        required
                    ></v-text-field>
                    <v-text-field
                        v-model="form.last"
                        :rules="rules.lastname"
                        color="accent"
                        label="Nom"
                        required
                    ></v-text-field>
                    <v-text-field
                        v-model="form.mail"
                        :rules="rules.mail"
                        color="accent"
                        label="Mail"
                        required
                    ></v-text-field>
                    <span class="justify-end">
                      <v-btn
                          text
                          color="error"
                          @click="dialog.value = false"
                      >Fermer</v-btn>
                      <v-btn
                          :disabled="!formIsValid"
                          text
                          color="accent"
                          type="submit"
                      >Sauvegarder</v-btn>
                    </span>
                  </v-form>
                </v-card-text>
                <v-card-actions class="justify-end">

                </v-card-actions>
              </v-card>
            </template>
          </v-dialog>
          <!-- ## POPUP MODIFICATION PROFIL ## -->
          <v-card-text>

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
          .col-6 .col-md-4
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
import Avatar from 'vue-avatar'

  const gradients = [
    ['#222'],
    ['#42b3f4'],
    ['red', 'orange', 'yellow'],
    ['purple', 'violet'],
    ['#00c6ff', '#F0F', '#FF0'],
    ['#f72047', '#ffd200', '#1feaea'],
  ]

  export default {
    name: 'Settings',

    components: {Avatar},

    data () {
      const profileForm = Object.freeze({
        first: '',
        last: '',
        mail: '',
      })

      return {
        form: Object.assign({}, profileForm),
        rules: {
          firstname: [val => (val || '').length > 0 || 'Ce champ ne doit pas être vide'],
          lastname: [val => (val || '').length > 0 || 'Ce champ ne doit pas être vide'],
          mail: [val => !val || /^\w+([.-]?\w+)*@\w+([.-]?\w+)*(\.\w{2,3})+$/.test(val) || 'L\'adresse mail doit être valide'],
        },
        width: 2,
        radius: 10,
        padding: 8,
        lineCap: 'round',
        gradient: gradients[1],
        value: [0, 2, 5, 9, 5, 10, 3, 5, 0, 0, 1, 8, 2, 9, 0],
        gradientDirection: 'top',
        gradients,
        fill: false,
        type: 'trend',
        autoLineWidth: false,
      }
    },

    computed: {
      formIsValid () {
        return (
            this.form.first &&
            this.form.last &&
            this.form.mail
        )
      },
    },

    methods: {
      resetForm () {
        this.form = Object.assign({}, this.profileForm)
        this.$refs.form.reset()
      },
      submit () {
        this.snackbar = true
        this.resetForm()
      },
    },

  }
</script>
