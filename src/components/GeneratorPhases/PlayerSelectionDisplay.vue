<template>
  <div class="outerContainer">
    <div class="teamsWrapper">
      <div v-for="(team, index) in teams" :key="index">
        Team {{ index + 1 }}
        <div
          class="teamWrapper"
          v-bind:style="{ height: wrapperHeight + 'vh' }"
        >
          <Avatar v-for="member in team" :text="member" :key="member" />
        </div>
      </div>
    </div>
    <v-row align-content="center">
      <v-col cols="auto">
        <v-btn @click="back">
          <v-icon color="black" class="pr-2">mdi-arrow-left-bold</v-icon
          >Back</v-btn
        >
      </v-col>
    </v-row>
  </div>
</template>

<script>
import Avatar from "@/components/General/Avatar";

export default {
  components: {
    Avatar,
  },
  props: {
    teams: Array,
  },
  computed: {
    wrapperHeight: function () {
      return 60 / this.teams.length - 4;
    },
  },
  methods: {
    generateTeams() {
      this.$emit("generateTeams", true);
    },
    back() {
      this.$emit("changePhase", 2);
    },
  },
};
</script>

<style scoped>
.teamsWrapper {
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  height: 63vh;
}

.teamWrapper {
  display: flex;
  border: 5px solid white;
  justify-content: space-evenly;
  align-items: center;
}
</style>
