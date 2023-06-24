<template>
  <v-container>
    <v-alert icon="mdi-account-multiple">
      Cantidad total de alumnos permitidos: {{ courses.reduce((accum, course) => accum + course.cupos, 0) }} alumnos.
    </v-alert>
  </v-container>
  <v-container>
    <v-alert icon="mdi-account-check">
      Cantidad total de alumnos inscritos: {{ courses.reduce((accum, course) => accum + course.inscritos, 0) }} alumnos.
    </v-alert>
  </v-container>
  <v-container>
    <v-alert icon="mdi-account-plus">
      Cantidad de cupos restantes: {{ courses.reduce((accum, course) => accum + (course.cupos - course.inscritos), 0) }} alumnos.
    </v-alert>
  </v-container>
  <v-container>
    <v-alert icon="mdi-cancel">
      Cantidad total de cursos terminados: {{ courses.filter(course => course.completado).length }} cursos.
    </v-alert>
  </v-container>
  <v-container>
    <v-alert icon="mdi-alarm-light">
      Cantidad total de cursos activos: {{ courses.filter(course => !course.completado).length }} cursos.
    </v-alert>
  </v-container>
  <v-container>
    <v-alert icon="mdi-alarm-light">
      Cantidad total de cursos: {{ courses.length }} cursos.
    </v-alert>
  </v-container>
</template>

<script>
import { useCourseStore } from "@/store/course.ts";
import { mapState } from "pinia";
const courseStore = useCourseStore();

export default {
  data() {
    return {
    };
  },
  computed: {
    ...mapState(useCourseStore, ["courses"]),
  }
};
</script>

<style>
</style>