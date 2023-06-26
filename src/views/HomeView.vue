<template>
  <v-container>
    <v-row justify="space-around">
      <v-col v-for="curso in cursos" :key="curso.id">
      <v-card width="350px" height="49rem" class="px-5 py-2">
        <v-img
          width="300px"
          height="300px"
          :src="curso.img"
        >

        </v-img>
        <v-card-title class="ml-7 text-size">
          {{curso.nombre}}
        </v-card-title>

        <v-card-text>
          <div class="font-weight-bold ml-8 mb-2">
            Información
          </div>

          <v-timeline
            align-top
            dense
          >
            <v-timeline-item
            color="purple"
            >
              <div>
                <div class="font-weight-normal">
                  <span>Costo: </span><strong>${{curso.costo}}</strong> 
                </div>
                <div class="font-weight-normal">
                  <span>Duración: {{curso.duracion}}</span> 
                </div>
              </div>
            </v-timeline-item>

            <v-timeline-item
            color="green"
            >
              <div>
                <div class="font-weight-normal">
                  <span>Cupos: </span><strong>{{curso.cupos}}</strong> 
                </div>
                <div class="font-weight-normal">
                  <span>Completado: {{curso.completado}}</span>
                </div>
              </div>
            </v-timeline-item>

            <v-timeline-item
            color="purple"
            >
              <div>
                <div class="font-weight-normal">
                  <span>Fecha de registro: </span>
                </div>
                <div class="font-weight-normal">
                  <span>{{curso.fecha_registro}}</span>
                </div>
              </div>
            </v-timeline-item>

                        <v-timeline-item
            color="green"
            >
              <div>
                <div class="font-weight-normal">
                  <span>Descripción: </span>
                </div>
                <div class="font-weight-normal">
                  <span>{{curso.descripcion}}</span>
                </div>
              </div>
            </v-timeline-item>
          </v-timeline>
        </v-card-text>
      </v-card>

      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import {mapState} from 'vuex'

  export default {
    name: 'home-view',
    computed:{
      ...mapState(['cursos'])
    },
    components: {
    },
  }
</script>
<style scoped>
.text-size{
  font-size: 1.1rem;
  font-weight: bold;
}
</style>
