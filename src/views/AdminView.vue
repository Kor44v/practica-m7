<template>
  <v-container>
    <v-row>
      <v-col>
        <h1 class="text-center">Administración</h1>
        <AddCurso></AddCurso>
        <v-simple-table class="mb-10">
          <template v-slot:default>
            <thead>
              <tr>
                <th class="text-left">Nombre</th>
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
              <tr v-for="curso in cursos" :key="curso.id">
                <td>{{ curso.nombre }}</td>
                <td>{{ curso.cupos }}</td>
                <td>{{ curso.inscritos }}</td>
                <td>{{ curso.duracion }}</td>
                <td>
                  <v-chip class="ma-2" color="green" text-color="white">
                    ${{ curso.costo }}
                  </v-chip>
                </td>
                <td>
                  <v-chip :color="curso.completado ? 'light-blue lighten-2' : 'grey lighten-1'" text-color="white">
                    {{ curso.completado ? "Si" : "No" }}
                  </v-chip>
                </td>
                <td>
                  <v-chip class="ma-2" color="green" text-color="white">
                    {{ curso.fecha_registro }}
                  </v-chip>
                </td>

                <td>
                  <v-btn
                    icon
                    color="orange"
                    @click="$router.push(`/edit/${curso.id}`)"
                    ><v-icon>mdi-pencil</v-icon></v-btn
                  >
                  <v-btn icon color="red" @click="openDialog(curso.nombre)"
                    ><v-icon>mdi-delete</v-icon></v-btn
                  >
                </td>
              </tr>
            </tbody>
          </template>
        </v-simple-table>
      </v-col>
    </v-row>
    <div>
      <v-alert
        icon="mdi-account-multiple"
        color="purple"
        outlined
        type="success"
        shaped
        dense
      >
        Vacantes totales
        {{ totalAllow }}
      </v-alert>

      <div>
        <v-alert
          icon="mdi-account-check"
          color="blue lighten-3"
          outlined
          type="success"
          shaped
          dense
        >
          Total Inscritos: {{ totalReg }}
        </v-alert>
      </div>
      <div>
        <v-alert
          icon="mdi-account-plus"
          color="red"
          outlined
          type="success"
          shaped
          dense
        >
          Total cupos restantes: {{ cuposRes }}
        </v-alert>
      </div>

      <div>
        <v-alert
          icon="mdi-cancel"
          color="pink lighten-3"
          outlined
          type="success"
          shaped
          dense
        >
          Cursos Terminados:{{ cursosTerminados }}
        </v-alert>
      </div>

      <div>
        <v-alert
          icon=" mdi-bell-ring"
          color="lime"
          outlined
          type="success"
          shaped
          dense
        >
          Cursos Activos: {{ cursosActivos }}
        </v-alert>
      </div>

      <div>
        <v-alert
          icon=" mdi-bell-ring"
          color="orange lighten-1"
          outlined
          type="success"
          shaped
          dense
        >
          Cursos totales: {{ totalCursos }}
        </v-alert>
      </div>
    </div>
    <v-dialog v-model="dialog" width="500">
      <v-card>
        <v-card-title class="text-h5 grey lighten-2">
          ¿Seguro que quieres eliminar este curso?
        </v-card-title>
        <v-divider></v-divider>

        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn color="primary" text @click="deleteCourse"> Eliminar </v-btn>
          <v-spacer></v-spacer>
          <v-btn color="primary" @click="dialog = false">Cerrar</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </v-container>
</template>

<script>
import AddCurso from "@/components/AddCurso.vue";
import { mapState, mapGetters, mapActions } from "vuex";
export default {
  name: "admin-view",
  created() {},
  data() {
    return {
      cupos_r: "",
      curso_activo: null,
      dialog: false,
      name: "",
    };
  },
  computed: {
    ...mapState(["cursos"]),
    ...mapGetters([
      "totalAllow",
      "totalReg",
      "cuposRes",
      "totalCursos",
      "cursosTerminados",
      "cursosActivos",
    ]),
  },
  props: {},
  methods: {
    ...mapActions(["delete_curso"]),
    openDialog(name) {
      console.log(name);
      this.dialog = true;
      this.name = name;
    },
    deleteCourse() {
      this.delete_curso(this.name);
      this.dialog = false;
    },
    test() {
      console.log("123");
    },
  },
  components: {
    AddCurso,
  },
};
</script>

<style lang="scss" scoped></style>
