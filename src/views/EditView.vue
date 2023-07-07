import { mapGetters } from 'vuex';
<template>
  <v-container>
    <v-row>
      <v-col>
        <v-form ref="form">
          <v-text-field
            label="Nombre"
            v-model="form.nombre"
            :rules="nameRules"
            required
          ></v-text-field>
          <v-text-field
            label="URL de la imagen"
            v-model="form.img"
            :rules="nameRules"
            required
          ></v-text-field>
          <v-text-field
            label="Cupos del curso"
            v-model="form.cupos"
            :rules="nameRules"
            type="number"
            required
          ></v-text-field>
          <v-text-field
            label="Inscritos en el curso"
            v-model="form.inscritos"
            :rules="inscritosRules"
            type="number"
            required
          ></v-text-field>
          <v-text-field
            label="Duración del curso"
            v-model="form.duracion"
            :rules="nameRules"
            required
          ></v-text-field>
          <v-text-field
            label="Fecha de registro"
            v-model="form.fecha_registro"
            :rules="nameRules"
            disabled
            required
          ></v-text-field>
          <v-text-field
            label="Costo del curso"
            v-model="form.costo"
            :rules="nameRules"
            required
          ></v-text-field>
          <v-text-field
            label="Estado del curso"
            v-model="form.completado"
            :rules="completadoRule"
            required
          ></v-text-field>
          <v-textarea
            label="Descripción del curso"
            v-model="form.descripcion"
            :rules="nameRules"
            required
          ></v-textarea>

          <v-btn color="success" class="mr-4" @click="editar" :disabled="!valid"> Editar </v-btn>

          <v-btn color="error" class="mr-4" @click="$router.push('/admin')"
            >Cerrar</v-btn
          >
          <v-btn color="primary" to="/admin"> Volver admin </v-btn>
        </v-form>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import { mapGetters, mapActions } from "vuex";
export default {
  name: "edit-view",
  created() {
    this.setForm();
  },
  data() {
    return {
      valid:true,
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
      completadoRule: [
        (v) => !!v || "Campo requerido",
        (v) => {
          if (v == "true") {
            this.form.inscritos = "0";
            console.log(this.form.inscritos);
          }
          return true;
        },
      ], //TODO:revisar condicion
    };
  },
  props: {
    id: {
      type: String,
      required: true,
    },
  },
  computed: {
    ...mapGetters(["getCourseById"]),
  },
  methods: {
    ...mapActions(["edit_curso"]),
    validate() {
      this.$refs.form.validate();
    },
    reset() {
      this.$refs.form.reset();
    },
    setForm() {
      let curso = this.getCourseById(this.id);
      console.log(this.id);
      this.form = curso;
    },
    editar() {
      this.validate();
      this.edit_curso(this.form);
      this.$router.push("/admin");
    },
  },
  components: {},
};
</script>

<style lang="scss" scoped></style>
