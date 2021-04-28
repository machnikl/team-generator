<template>
  <div>
    <v-row class="logoContainer">
      <v-col cols="12">
        <v-img
          :src="require('../assets/logo2.svg')"
          class="mt-6"
          contain
          height="80"
        />
      </v-col>
    </v-row>
  </div>
</template>

<script>
export default {};
</script>

<style scoped>
.logoContainer {
  height: 24vh;
}
</style>
