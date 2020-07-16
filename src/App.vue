<template>
  <v-app id="inspire" dark>
    <v-navigation-drawer
            v-model="drawer"
            app
            clipped
            dark
    >
      <v-list dense>
        <v-list-item link>
          <v-list-item-action>
            <v-icon>fa-list</v-icon>
          </v-list-item-action>
          <v-list-item-content>
            <v-list-item-title>Match View</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
        <v-list-item link>
          <v-list-item-action>
            <v-icon>fa-robot</v-icon>
          </v-list-item-action>
          <v-list-item-content>
            <v-list-item-title>OPR View</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

    <v-app-bar
            app
            clipped-left
            dark
    >
      <v-app-bar-nav-icon @click.stop="drawer = !drawer"></v-app-bar-nav-icon>
      <v-toolbar-title>Match View</v-toolbar-title>
    </v-app-bar>

    <v-main
    dark>

      <v-container
              class="fill-height"
              fluid
              dark

      >
        <datatable
        ></datatable>
      </v-container>
    </v-main>

    <v-footer app>
      <span>&copy; {{ new Date().getFullYear() }}</span>
    </v-footer>
  </v-app>
</template>

<script>
import datatable from './components/DataTable'
  export default {

  components:
          {
            datatable
          },
    props: {
      source: String,
    },
    data: () => ({
      drawer: null,
    }),
    created () {
      this.$vuetify.theme.light = true
    },
  }
</script>