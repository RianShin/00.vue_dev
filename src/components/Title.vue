<template>
  <v-toolbar-title>
    {{ title }}
    <v-btn icon @click="openDialog"><v-icon>mdi-pencil</v-icon></v-btn>
    <v-dialog v-model="dialog" max-width="400" >
      <v-card-title>
        modify title
      <v-spacer/>
        <v-btn icon @click="save"><v-icon>mdi-content-save</v-icon></v-btn>
        <v-btn icon @click="dialog=false"><v-icon>mdi-close</v-icon></v-btn>
      </v-card-title>

      <v-card-text>
        <v-text-field v-model="text" outlined label="title" @keypress.enter="save"/>
      </v-card-text>
    </v-dialog>
  </v-toolbar-title>
</template>

<script>
export default {
  props: ['title'],
  data () {
    return {
      dialog: false,
      text: this.title
    }
  },
  methods: {
    openDialog () {
      this.dialog = true
    },
    async save () {
      // try {
      //   await this.$firebase.database().ref().child('site').update({ title: this.text })
      // } catch (e) {
      //   console.log(e.message)
      // } finally {
      //   this.dialog = false
      // }
      try {
        await this.$firebase.database().ref().child('site').update({ title: this.text })
      } finally {
        this.dialog = false
      }
    }
  }
}
</script>
