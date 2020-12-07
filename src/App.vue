<template>
  <v-app>
    <v-app-bar
      app
      color="primary"
      dart
      >
      <v-app-bar-nav-icon @click="drawer=!drawer"/>
      <site-title :title="title"></site-title>
      <v-spacer/>
      <v-btn icon @click="save"><v-icon>mdi-check</v-icon></v-btn>
    </v-app-bar>
    <v-navigation-drawer app v-model="drawer">
      test
      <site-menu></site-menu>
    </v-navigation-drawer>
    <v-content>
      <router-view/>
    </v-content>
    <site-footer :footer="footer"></site-footer>
  </v-app>
</template>

<script>
import SiteTitle from '@/components/Title'
import SiteFooter from '@/components/Footer'
import SiteMenu from '@/components/Menu'

export default {
  components: { SiteTitle, SiteFooter, SiteMenu },
  name: 'App',
  data () {
    return {
      drawer: false,
      items: [],
      title: 'my Title',
      footer: 'my footer'
    }
  },
  created () {
  },
  mounted () {
    console.log(this.$firebase)
  },
  methods: {
    save () {
      console.log('save0000000')
      this.$firebase.database().ref().child('abcd').set({
        title: 'title',
        text: 'text'
      })
    }
  }
}
</script>
