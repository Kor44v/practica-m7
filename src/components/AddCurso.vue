<template>
  <v-row justify="center">
    <v-dialog
      v-model="dialog"
      persistent
      max-width="600px"
    >
      <template v-slot:activator="{ on, attrs }">
        <v-btn
          color="primary"
          dark
          v-bind="attrs"
          v-on="on"
          class="my-10 py-5"
        >
          AGREGAR CURSO
        </v-btn>
      </template>
      <v-card>
        <v-card-title>
          <span class="text-h5">Cursos a agregar</span>
        </v-card-title>
        <v-card-text>
          <v-form ref="form" >
          <v-container>
            <v-row>
              <v-col
                cols="12"
                sm="6"
                md="4"
              >
                <v-text-field
                  label="Nombre"
                  v-model="form.nombre"
                  required
                ></v-text-field>
              </v-col>
              <v-col
                cols="12"
                sm="6"
                md="4"
              >
                <v-text-field
                  label="URL de la imagen"
                  v-model="form.img"
                  required
                ></v-text-field>
              </v-col>
              <v-col
                cols="12"
                sm="6"
                md="4"
              >
                <v-text-field
                  label="Cupos del curso"
                  v-model="form.cupos"
                  required
                ></v-text-field>
              </v-col>
              <v-col cols="12">
                <v-text-field
                  label="Inscritos en el curso"
                  v-model="form.inscritos"
                  required
                ></v-text-field>
              </v-col>
              <v-col cols="12">
                <v-text-field
                  label="Duración del curso"
                  v-model="form.duracion"
                  required
                ></v-text-field>
              </v-col>
              <v-col
                cols="12"
                sm="6"
              >
              <v-text-field
                  label="Fecha de registro"
                  v-model="form.fecha_registro"
                  required
                ></v-text-field>
              </v-col>
              <v-col
                cols="12"
                sm="6"
              >
                <v-text-field
                  label="Costo del curso"
                  v-model="form.costo"
                  required
                ></v-text-field>
              </v-col>

              <v-col
                cols="12"
              >
                <v-textarea
                  label="Descripción del curso"
                  v-model="form.descripcion"
                  required
                ></v-textarea>
              </v-col>
            </v-row>
          </v-container>
          </v-form>
        </v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn>Agregar</v-btn>
          <v-btn
            color="blue darken-1"
            text
            @click="dialog = false"
          >
            Close
          </v-btn>
          <v-btn
            color="blue darken-1"
            text
            @click="clean"
          >
            Limpiar Formulario
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </v-row>
</template>
<script>
export default {
  name: "addCurso-comp",
  created() {},
  data() {
    return {
      dialog: false,
      form:{
      nombre:'',
      img:'',
      cupos:'',
      inscritos:'',
      duracion:'',
      fecha_registro:'',
      costo:'',
      descripcion:'',

      }
    };

  },
  props: {},
  methods: {
    clean(){
      this.$refs.form.reset()
    }
  },
};
</script>

<style lang="scss" scoped></style>