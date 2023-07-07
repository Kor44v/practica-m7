<template>
  <div>
    <v-app-bar
      color="deep-purple accent-4"
      dense
      dark
    >


      <v-toolbar-title @click="$router.push('/')">
        Cursos AlphaTauri
      </v-toolbar-title>

      <v-spacer></v-spacer>


      <v-btn icon to="/" >
        <v-icon>mdi-home</v-icon>
      </v-btn>

      <v-btn icon to="/admin">
        <v-icon>mdi-wrench</v-icon>
      </v-btn>


    </v-app-bar>
  </div>
</template>

<script>
export default {
  name: "navbar-comp",
  created() {},
  data() {
    return {};
  },
  props: {},
  methods: {},
};
</script>

<style lang="scss" scoped></style>