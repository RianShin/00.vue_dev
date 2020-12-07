<template>
  <v-app>
    <div id="app">
      title modify
      <div id="nav">
        <router-link to="/">home</router-link> |
        <router-link to="/about">about</router-link> |
        <router-link to="/test">test</router-link>
      </div>
      <router-view/>
    </div>
  </v-app>
</template>

<script>
</script>
