<template>
  <v-row justify="center">
    <v-dialog
      v-model="dialog"
      persistent
      max-width="600px"
      @click:outside="dialog = false"
    >
      <template v-slot:activator="{ on, attrs }">
        <v-btn color="primary" dark v-bind="attrs" v-on="on" class="my-10 py-5">
          AGREGAR CURSO
        </v-btn>
      </template>
      <v-card>
        <v-card-title>
          <span class="text-h5">Cursos a agregar</span>
        </v-card-title>
        <v-card-text>
          <v-form ref="form">
            <v-container>
              <v-row>
                <v-col cols="12" sm="6" md="4">
                  <v-text-field
                    label="Nombre"
                    v-model="form.nombre"
                    :rules="nameRules"
                    required
                  ></v-text-field>
                </v-col>
                <v-col cols="12" sm="6" md="4">
                  <v-text-field
                    label="URL de la imagen"
                    v-model="form.img"
                    :rules="nameRules"
                    required
                  ></v-text-field>
                </v-col>
                <v-col cols="12" sm="6" md="4">
                  <v-text-field
                    label="Cupos del curso"
                    v-model="form.cupos"
                    :rules="nameRules"
                    type="number"
                    required
                  ></v-text-field>
                </v-col>
                <v-col cols="12">
                  <v-text-field
                    label="Inscritos en el curso"
                    v-model="form.inscritos"
                    :rules="inscritosRules"
                    type="number"
                    required
                  ></v-text-field>
                </v-col>
                <v-col cols="12">
                  <v-text-field
                    label="Duración del curso"
                    v-model="form.duracion"
                    :rules="nameRules"
                    required
                  ></v-text-field>
                </v-col>
                <v-col cols="12" sm="6">
                  <v-text-field
                    label="Fecha de registro"
                    v-model="form.fecha_registro"
                    :rules="nameRules"
                    disabled
                    required
                  ></v-text-field>
                </v-col>
                <v-col cols="12" sm="6">
                  <v-text-field
                    label="Costo del curso"
                    v-model="form.costo"
                    :rules="nameRules"
                    required
                  ></v-text-field>
                </v-col>
                <v-col cols="12">
                  <v-textarea
                    label="Descripción del curso"
                    v-model="form.descripcion"
                    :rules="nameRules"
                    required
                  ></v-textarea>
                </v-col>
              </v-row>
            </v-container>
          </v-form>
        </v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn color="blue darken-1" text @click="add"> Agregar </v-btn>
          <v-btn color="blue darken-1" text @click="dialog = false">
            Cancelar
          </v-btn>
          <v-btn color="blue darken-1" text @click="clean">
            Limpiar Formulario
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </v-row>
</template>
<script>
import { mapActions } from "vuex";

export default {
  name: "addCurso-comp",
  created() {},
  data() {
    return {
      dialog: false,
      form: {
        id: "",
        nombre: "",
        img: "",
        cupos: null,
        inscritos: null,
        duracion: "",
        fecha_registro: new Date().toDateString(),
        costo: null,
        descripcion: "",
        completado: false,
      },
      nameRules: [(v) => !!v || "Campo requerido"],
      inscritosRules: [
        (v) => !!v || "Campo requerido",
        (v) => {
          if (Number(v) > Number(this.form.cupos))
            return "El numero de inscritos no puede ser mayor al de cupos";
          return true;
        },
      ],
    };
  },
  props: {},
  methods: {
    ...mapActions(["add_curso"]),
    add() {
      console.log(this.form);
      const newForm = Object.assign({}, this.form); // Crear una nueva instancia del objeto form
      this.add_curso(newForm);
      this.dialog = false;
      this.clean();
    },
    clean() {
      this.$refs.form.reset();
    },
    // generateId(){
    //   let id = this.totalCursos+1
    //   console.log(this.totalCursos)
    //   return this.form.id = id
    // }
  },
};
</script>

<style lang="scss" scoped></style>
