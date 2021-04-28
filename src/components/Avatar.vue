<template>
  <transition name="fade">
    <v-avatar color="#133147" light size="56" class="avatarStyle ml-4 mt-3">
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
  background: #348ac7;
  box-shadow: 20px 20px 60px #2c75a9, -20px -20px 60px #3c9fe5;
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
