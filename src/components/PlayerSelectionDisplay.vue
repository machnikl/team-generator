<template>
  <div>
    <div v-for="(team, index) in teams" :key="team">
      <div class="teamWrapper" v-bind:style="{ height: wrapperHeight + 'vh' }">
        <Avatar v-for="member in team" :text="member" :key="member" />
      </div>
      <v-avatar
        v-if="index < teams.length - 1"
        color="white"
        light
        size="80"
        class="versusStyle"
        v-bind:style="{ top: wrapperHeight + 16 + 'vh' }"
      >
        VS
      </v-avatar>
    </div>
  </div>
</template>

<script>
import Avatar from "@/components/Avatar";

export default {
  components: {
    Avatar,
  },
  props: ["teams"],
  computed: {
    wrapperHeight: function () {
      return 70 / this.teams.length;
    },
  },
};
</script>

<style scoped>
.teamWrapper {
  border: 5px solid white;
}

.versusStyle {
  position: absolute;
  left: 50%;
  -webkit-transform: translateX(-50%);
  transform: translateX(-50%);
  color: black;
  font-weight: bold;
  font-size: 24px;
}
</style>
