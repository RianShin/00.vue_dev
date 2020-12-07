<template>
  <v-app>
<!--    <div id="app">-->
<!--      title modify-->
<!--      <div id="nav">-->
<!--        <router-link to="/">home</router-link> |-->
<!--        <router-link to="/about">about</router-link> |-->
<!--        <router-link to="/test">test</router-link>-->
<!--      </div>-->
<!--      <router-view/>-->
<!--    </div>-->
    <v-app-bar
      app
      color="primary"
      dart
      >
      <v-app-bar-nav-icon @click="drawer=!drawer"></v-app-bar-nav-icon>
      <v-toolbar-title>page title</v-toolbar-title>
      <v-spacer/>
      <v-btn icon to="/about">
        <v-icon>mdi-magnify</v-icon>
      </v-btn>
    </v-app-bar>
    <v-navigation-drawer app v-model="drawer">
      test
      <v-list-item>
        <v-list-item-content>
          <v-list-item-title class="title">
            Application
          </v-list-item-title>
          <v-list-item-subtitle>
            subtext
          </v-list-item-subtitle>
        </v-list-item-content>
      </v-list-item>
      <v-divider></v-divider>
    </v-navigation-drawer>
    <v-content>
      <router-view/>
    </v-content>
    <v-footer app color="primary" absolute>
      <v-spacer/>
      <div>&copy; {{ new Date().getFullYear() }}</div>
    </v-footer>
  </v-app>
</template>

<script>
export default {
  name: 'App',
  data () {
    return {
      drawer: false
    }
  }
}
</script>
