<template>
  <v-footer app color="primary" dark absolute :footer="footer">
    <v-spacer/>
    <div>&copy; {{ new Date().getFullYear() + ' ' + footer }}</div>
    <v-btn icon @click="openDialog"><v-icon>mdi-pencil</v-icon></v-btn>
    <v-dialog v-model="dialog" max-width="400" >
      <v-card-title>
        modify title
        <v-spacer/>
        <v-btn icon @click="save"><v-icon>mdi-content-save</v-icon></v-btn>
        <v-btn icon @click="dialog=false"><v-icon>mdi-close</v-icon></v-btn>
      </v-card-title>

      <v-card-text>
        <v-text-field v-model="text" outlined label="footer" @keypress.enter="save"/>
      </v-card-text>
    </v-dialog>
  </v-footer>
</template>

<script>
export default {
  props: ['footer'],
  data () {
    return {
      dialog: false,
      text: this.footer
    }
  },
  methods: {
    openDialog () {
      this.dialog = true
    },
    async save () {
      // console.log('[this.footer]' + this.footer)
      try {
        await this.$firebase.database().ref().child('site').update({ footer: this.text })
      } catch (e) {
        console.log(e.message)
      } finally {
        this.dialog = false
      }
    }
  }
}
</script>
