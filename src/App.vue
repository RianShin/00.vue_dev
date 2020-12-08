<template>
  <v-app>
    <v-app-bar
      app
      color="primary"
      dart
      >
      <v-app-bar-nav-icon @click="drawer = !drawer"/>
      <site-title :title="site.title"></site-title>
      <v-spacer/>
<!--      <v-btn icon @click="save"><v-icon>mdi-check</v-icon></v-btn>-->
<!--      <v-btn icon @click="read"><v-icon>mdi-access-point</v-icon></v-btn>-->
<!--      <v-btn icon @click="readOnce"><v-icon>mdi-access-point-network</v-icon></v-btn>-->
    </v-app-bar>
    <v-navigation-drawer app v-model="drawer" width="400">
      test
      <site-menu :items="site.menu"></site-menu>
    </v-navigation-drawer>
    <v-content>
      <router-view/>
    </v-content>
    <site-footer :footer="site.footer"></site-footer>
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
      site: {
        menu: [
          {
            title: 'home',
            icon: 'mdi-home',
            subItems: [
              {
                title: 'Dashboard',
                to: '/'
              },
              {
                title: 'About',
                to: '/about'
              }
            ]
          },
          {
            title: 'about',
            active: true,
            icon: 'mdi-pencil',
            subItems: [
              {
                title: 'About',
                to: '/about'
              }
            ]
          }
        ],
        title: 'my Title',
        footer: 'my footer'
      }
    }
  },
  created () {
    this.subscribe()
  },
  mounted () {
    console.log(this.$firebase)
  },
  methods: {
    subscribe () {
      console.log('subscribe')
      this.$firebase.database().ref().child('site').on('value', (sn) => {
        console.log(sn)
        console.log(sn.val())
        const v = sn.val()
        if (!v) {
          this.$firebase.database().ref().child('site').set(this.site)
          // return
        }
        this.site = v
      }, (e) => {
        console.log(e.message)
      })
    }
    // ,
    // save () {
    //   console.log('save0000000')
    //   this.$firebase.database().ref().child('abcd').set({
    //     title: 'title',
    //     text: 'text'
    //   })
    // },
    // read () {
    //   console.log('load0000000')
    //   this.$firebase.database().ref().child('abcd').on('value', (sn) => {
    //     console.log(sn)
    //     console.log(sn.val())
    //   })
    // },
    // async readOnce () {
    //   console.log('load0000000')
    //   const sn = await this.$firebase.database().ref().child('abcd').once('value')
    //   console.log(sn)
    //   console.log(sn.val())
    // }
  }
}
</script>
