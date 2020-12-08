<template>
  <v-progress-circular indeterminate v-if="loading"></v-progress-circular>
  <v-menu offset-y v-else-if="!$store.state.fireUser">
    <template v-slot:activator="{ on }">
      <v-btn icon v-on="on"><v-icon>mdi-account</v-icon></v-btn>
    </template>
    <v-card>
      <v-card-title>login</v-card-title>
      <v-divider/>
      <v-card-actions>
        <v-btn color="red" dark @click="signInWithGoogle" block><v-icon left>mdi-google</v-icon>google login</v-btn>
      </v-card-actions>
      <v-card-actions>
        <v-btn color="blue" dark @click="signInWithFB" block><v-icon left>mdi-google</v-icon>FB login</v-btn>
      </v-card-actions>
<!--      <v-card-actions>-->
<!--        <v-btn color="black" dark @click="signOut" block><v-icon left></v-icon>logout</v-btn>-->
<!--      </v-card-actions>-->
    </v-card>
  </v-menu>
  <v-menu offset-y v-else>
    <template v-slot:activator="{ on }">
      <v-btn icon v-on="on">
<!--        <v-icon>mdi-account</v-icon>-->
        <v-avatar size="24">
          <v-img :src="$store.state.fireUser.photoURL"></v-img>
        </v-avatar>
      </v-btn>
    </template>
    <v-card>
      <v-card-title>login</v-card-title>
      <v-divider/>
<!--      <v-card-actions>-->
<!--        <v-btn color="red" dark @click="signInWithGoogle" block><v-icon left>mdi-google</v-icon>google login</v-btn>-->
<!--      </v-card-actions>-->
      <v-card-title>정보</v-card-title>
      <v-card-actions>
        <v-btn color="black" dark @click="signOut" block><v-icon left></v-icon>logout</v-btn>
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
        this.$store.commit('setFireUser', sn.user)
        console.log(sn.user)
      } finally {
        this.loading = false
      }
    },
    signOut () {
      this.$firebase.auth().signOut()
    },
    signInWithFB () {
      throw Error('next To-do ')
    }
  }
}
</script>
