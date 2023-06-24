<template>
  <v-app-bar>
    <v-app-bar-nav-icon></v-app-bar-nav-icon>
    <v-app-bar-title> Cursos AlfaWeb </v-app-bar-title>
    <v-spacer></v-spacer>
    <router-link to="/">
      <v-btn icon>
        <v-icon>mdi-home</v-icon>
      </v-btn>
    </router-link>
    <router-link to="/admin">
      <v-btn icon>
        <v-icon>mdi-tools</v-icon>
      </v-btn>
    </router-link>
  </v-app-bar>
</template>

<script lang="ts" setup>
</script>
