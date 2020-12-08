<template>
  <v-menu offset-y>
    <template v-slot:activator="{ on }">
      <v-btn icon v-on="on"><v-icon>mdi-account</v-icon></v-btn>
    </template>
    <v-card>
      <v-card-title>login</v-card-title>
      <v-divider/>
      <v-card-actions>
        <v-btn color="red" dark @click="signInWithGoogle"><v-icon left>mdi-google</v-icon>google login</v-btn>
      </v-card-actions>
    </v-card>
  </v-menu>
<!--  <v-btn icon><v-icon>mdi-account</v-icon></v-btn>-->
</template>

<script>
export default {
  data () {
    return {
      loading: false
    }
  },
  methods: {
    async signInWithGoogle () {
      const provider = new this.$firebase.auth.GoogleAuthProvider()
      this.$firebase.auth().languageCode = 'ko'
      this.loading = true
      try {
        const sn = await this.$firebase.auth().signInWithPopup(provider)
        // this.$store.commit('setFireUser', sn.user)
        console.log(sn.user)
      } finally {
        this.loading = false
      }
    },
    signOut () {
      this.$firebase.auth().signOut()
    }
  }
}
</script>
