<template>
    <v-container class="d-flex justify-center">
      <h1>Administrador</h1>
    </v-container>
    <AdminCursos></AdminCursos>
    <AdminStatsCursos></AdminStatsCursos>
</template>

<script lang="ts" setup>
  import AdminCursos from '@/components/AdminCursos.vue'
  import AdminStatsCursos from '@/components/AdminStatsCursos.vue'
</script>

<style>

</style>