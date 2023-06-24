<template>
  <v-container class="bg-surface-variant h-100">
    <v-container class="d-flex justify-center">
      <h1>Lista de cursos</h1>
    </v-container>
    <v-container>
      <v-row no-gutters>
        <v-col v-for="course in courses" :key="course.name" cols="12" sm="4">
          <v-container>
            <v-card width="350" class="pa-md-5">
              <template v-slot:title>
                <v-img height="150" aspect-ratio="1" :src="course.img"></v-img>
              </template>

              <template v-slot:subtitle>
                <v-container class="pt-4">
                  <h3>{{ course.nombre }}</h3>
                </v-container>
              </template>

              <template v-slot:text>
                Información
                <v-timeline side="end">
                  <v-timeline-item size="small" dot-color="blue">
                    <p><b>Costo:</b> ${{ course.costo }}</p>
                    <p><b>Duración:</b> {{ course.duracion }}</p>
                  </v-timeline-item>
                  <v-timeline-item size="small" dot-color="blue">
                    <p><b>Cupos:</b> {{ course.cupos }}</p>
                    <p>
                      <b>Completado:</b> {{ course.completado ? "Si" : "No" }}
                    </p>
                  </v-timeline-item>
                  <v-timeline-item size="small" dot-color="blue">
                    <p><b>Fecha de Registro</b></p>
                    <p>{{ course.fecha_registro }}</p>
                  </v-timeline-item>
                  <v-timeline-item size="small" dot-color="blue">
                    <p><b>Descripción</b></p>
                    <p>{{ course.descripcion }}</p>
                  </v-timeline-item>
                </v-timeline>
              </template>
            </v-card>
          </v-container>
        </v-col>
      </v-row>
    </v-container>
  </v-container>
</template>

<script>
import { useCourseStore } from "@/store/course.ts";
import { mapState } from "pinia";
export default {
  data() {
    return {};
  },
  computed: {
    ...mapState(useCourseStore, ["courses"]),
  },
};
</script>

<style>
</style>