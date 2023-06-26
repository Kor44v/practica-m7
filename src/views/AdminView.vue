<template>
<v-container>
  <v-row>
    <v-col>
        <AddCurso></AddCurso>
      <v-simple-table>
        <template v-slot:default>
          <thead>
            <tr>
              <th class="text-left">
                Nombre
              </th>
              <th class="text-left">
                Cupos
              </th>
              <th class="text-left">
                Inscritos
              </th>
              <th class="text-left">
                Duración
              </th>
              <th class="text-left">
                Costo
              </th>
              <th class="text-left">
                Terminado
              </th>
              <th class="text-left">
                Fecha
              </th>
              <th class="text-left">
                Acciones
              </th>
            </tr>
          </thead>
          <tbody>
            <tr
              v-for="curso in cursos"
              :key="curso.id"
            >
              <td>{{ curso.nombre }}</td>
              <td>{{ curso.cupos }}</td>
              <td>{{ curso.inscritos }}</td>
              <td>{{ curso.duracion }}</td>
              <td>{{ curso.costo}}</td>
              <td>{{ curso.completado }}</td>
              <td>{{ curso.fecha_registro }}</td>

              <td>                
                <v-btn icon><v-icon>mdi-pencil</v-icon></v-btn>
                <v-btn icon><v-icon>mdi-delete</v-icon></v-btn>
              </td>
            </tr>
          </tbody>
        </template>
      </v-simple-table>
    </v-col>
  </v-row>
  <div>
    Vacantes totales
    {{ totalAllow}}

    <div>
      Total Inscritos: {{totalReg}}
    </div>
    <div>
      Total cupos restantes: {{cuposRes}}
    </div>

    <div>
      Cursos Terminados:{{cursosTerminados}}
    </div>

    <div>
      Cursos Activos: 
    </div>

    <div>
      Cursos totales: {{totalCursos}}
    </div>
  </div>
</v-container>
</template>

<script>
import AddCurso from '@/components/AddCurso.vue';
import {mapState,mapGetters} from 'vuex'
export default {
  name: "admin-view",
  created() {},
  data() {
    return {
      cupos_r:''
    };
  },
  computed:{
    ...mapState(['cursos']),
    ...mapGetters(['totalAllow','totalReg','cuposRes','totalCursos','cursosTerminados'])
  },
  props: {},
  methods: {
  },
  components:{
    AddCurso
  }
};
</script>

<style lang="scss" scoped></style>