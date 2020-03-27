<template>
  <v-app light>
    <v-content>
      <v-container fill-height>
        <nuxt />
      </v-container>
    </v-content>
    <v-footer :fixed="fixed" app>
      <span>&copy; {{ new Date().getFullYear() }} Fixpoint, Inc.</span>
    </v-footer>
  </v-app>
</template>

<script>
export default {}
</script>
