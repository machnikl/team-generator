<template>
  <v-avatar color="#133147" light size="56" class="avatarStyle ml-4 mt-3">
    {{ text }}
  </v-avatar>
</template>

<script>
export default {
  props: ["text"],
};
</script>

<style scoped>
.avatarStyle {
  border: 5px solid white;
  font-weight: bolder;
  letter-spacing: 2px;
}
</style>
