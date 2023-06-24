<template>
  <v-container class="d-flex justify-center">
    <v-btn @click="overlay = !overlay" color="success">Agregar Curso</v-btn>
    <v-overlay v-model="overlay" contained class="align-center justify-center">
      <v-container class="bg-surface-variant mt-2">
        <v-sheet width="600">
          <v-form @submit.prevent class="pa-md-5">
            <v-text-field v-model="curso.nombre" label="Nombre"></v-text-field>
            <v-text-field v-model="curso.img" label="Url de la imagen"></v-text-field>
            <v-text-field v-model="curso.cupos" type="number" label="Cupos del curso"></v-text-field>
            <v-text-field v-model="curso.inscritos" type="number" label="Inscritos en el curso"></v-text-field>
            <v-text-field v-model="curso.duracion" label="Duración del curso"></v-text-field>
            <v-text-field v-model="curso.fecha_registro" label="Fecha de registro"></v-text-field>
            <v-checkbox v-model="curso.completado" label="Terminado"></v-checkbox>
            <v-text-field v-model="curso.costo" type="number" label="Costo del curso"></v-text-field>
            <v-textarea v-model="curso.descripcion" label="Descripción del curso"></v-textarea>
            <v-container class="d-flex justify-space-around">
              <v-btn color="success" type="submit" @click="save">Submit</v-btn>
              <v-btn color="default" @click="clean">Limpiar</v-btn>
              <v-btn color="error" @click="overlay = false">
                Cancelar
              </v-btn>
            </v-container>
          </v-form>
        </v-sheet>
      </v-container>
    </v-overlay>
  </v-container>

  <v-container>
    <v-table>
      <thead>
        <tr>
          <th class="text-left">Curso</th>
          <th class="text-left">Cupos</th>
          <th class="text-left">Inscritos</th>
          <th class="text-left">Duración</th>
          <th class="text-left">Costo</th>
          <th class="text-left">Terminado</th>
          <th class="text-left">Fecha</th>
          <th class="text-left">Acciones</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="course in courses" :key="course.name">
          <td>{{ course.nombre }}</td>
          <td>{{ course.cupos }}</td>
          <td>{{ course.inscritos }}</td>
          <td>{{ course.duracion }}</td>
          <td>
            <v-chip>${{ course.costo }}</v-chip>
          </td>
          <td>
            <v-chip>{{ course.terminado ? "Si" : "No" }}</v-chip>
          </td>
          <td>
            <v-chip>{{ course.fecha_registro }}</v-chip>
          </td>
          <td>
            <v-btn @click="getCourse(course.id)">
              <v-icon>mdi-pencil</v-icon>
            </v-btn>
            <v-btn @click="remove(course.id)">
              <v-icon>mdi-delete</v-icon>
            </v-btn>
          </td>
        </tr>
      </tbody>
    </v-table>
  </v-container>
</template>

<script>
import { useCourseStore } from "@/store/course.ts";
import { mapState } from "pinia";
const courseStore = useCourseStore();

export default {
  data() {
    return {
      overlay: false,
      curso: {
        nombre: "Nuevo curso de Sans",
        img: "https://easydrawingguides.com/wp-content/uploads/2020/08/Sans-from-Undertale-Step-10.png",
        cupos: 30,
        inscritos: 10,
        duracion: "11 meses",
        fecha_registro: "12/10/1992",
        completado: false,
        costo: 69000,
        descripcion: "El curso de Sans es muy divertido para la gente que le gustan los videojuegos"
      }
    };
  },
  computed: {
    ...mapState(useCourseStore, ["courses"]),
  },
  methods: {
    save() {
      if(!this.curso.id) {
        this.curso.id = Date.now();
        courseStore.create(this.curso);
      } else {
        courseStore.update(this.curso);
      }
      this.clean();
      this.overlay = false;
    },
    getCourse(id) {
      this.curso = { 
        ...this.courses.find(course => course.id == id)
      };
      this.overlay = true;
    },
    clean() {
      this.curso = {
        id: null,
        nombre: "",
        img: "",
        cupos: 0,
        inscritos: 0,
        duracion: "",
        fecha_registro: "",
        completado: true,
        costo: 0,
        descripcion: ""
      }
    },
    remove(id) {
      courseStore.delete(id)
    }
  }
};
</script>

<style>
</style>