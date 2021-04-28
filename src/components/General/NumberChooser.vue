<template>
  <div class="numberChooserContainer">
    <v-btn
      icon
      class="arrowStyle"
      @click="changeValue('minus')"
      :disabled="number < 3"
    >
      <v-icon color="white">mdi-minus-circle</v-icon>
    </v-btn>
    <span class="numberStyle pl-7"
      ><span>{{ number }}</span>
      <v-icon color="white" class="headerIcon">{{ iconName }}</v-icon></span
    >
    <v-btn
      icon
      class="arrowStyle"
      @click="changeValue('plus')"
      :disabled="number > 3"
    >
      <v-icon color="white">mdi-plus-circle</v-icon>
    </v-btn>
  </div>
</template>

<script>
export default {
  props: {
    iconName: String,
  },
  data() {
    return {
      number: 2,
    };
  },
  methods: {
    changeValue(operation) {
      if (operation === "minus") {
        this.number--;
      } else {
        this.number++;
      }
      this.$emit("valueChange", this.number);
    },
  },
};
</script>

<style scoped>
.numberChooserContainer {
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: center;
  margin-top: 16px;
  margin-bottom: 16px;
}

.numberStyle {
  font-size: 64px;
}

.headerIcon {
  padding-left: 8px;
  font-size: 24px;
  position: relative;
  left: -11px;
  bottom: 40px;
}
</style>
