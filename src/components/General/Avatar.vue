<template>
  <div class="avatarStyle mx-2">
    {{ text }}
  </div>
</template>

<script>
export default {
  props: {
    text: String,
  },
};
</script>

<style scoped>
.avatarStyle {
  font-weight: bolder;
  padding: 5px;
  letter-spacing: 2px;
  background: transparent !important;
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
