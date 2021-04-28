<template>
  <transition name="fade">
    <v-avatar color="#133147" light size="56" class="avatarStyle mx-2 mt-4">
      {{ text }}
    </v-avatar>
  </transition>
</template>

<script>
export default {
  props: ["text"],
};
</script>

<style scoped>
.avatarStyle {
  font-weight: bolder;
  letter-spacing: 2px;
  background: transparent !important;
  border: 3px solid white !important;
  text-transform: uppercase;
  animation: expand 0.5s ease-in-out;
}

@keyframes expand {
  from {
    transform: scale(0);
    opacity: 0;
    background: #5470b0;
  }
}
</style>
