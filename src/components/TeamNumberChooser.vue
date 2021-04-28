<template>
  <div>
    <h1 class="text-center">Teams Configurator</h1>
    <h2 class="text-center">
      How many teams?
      <v-icon color="white" class="headerIcon">mdi-account-group</v-icon>
    </h2>
    <div class="numberChooserContainer">
      <v-btn icon class="arrowStyle" @click="numberOfTeams--">
        <v-icon color="white">mdi-arrow-left-bold</v-icon>
      </v-btn>
      <span class="numberStyle px-4">{{ numberOfTeams }}</span>
      <v-btn icon class="arrowStyle" @click="numberOfTeams++">
        <v-icon color="white">mdi-arrow-right-bold</v-icon>
      </v-btn>
    </div>
    <h2 class="text-center">
      Players per Team?
      <v-icon color="white" class="headerIcon">mdi-account-question</v-icon>
    </h2>
    <div class="numberChooserContainer">
      <v-btn icon class="arrowStyle" @click="numberOfPlayersPerTeam--">
        <v-icon color="white">mdi-arrow-left-bold</v-icon>
      </v-btn>
      <span class="numberStyle px-4">{{ numberOfPlayersPerTeam }}</span>
      <v-btn icon class="arrowStyle" @click="numberOfPlayersPerTeam++">
        <v-icon color="white">mdi-arrow-right-bold</v-icon>
      </v-btn>
    </div>
    <v-row justify="space-around" class="mt-8">
      <v-col cols="auto">
        <v-btn @click="back">
          <v-icon color="black" class="pr-2">mdi-arrow-left-bold</v-icon
          >Back</v-btn
        >
      </v-col>
      <v-col cols="auto">
        <v-btn @click="generateTeams">Generate Teams</v-btn>
      </v-col>
    </v-row>
  </div>
</template>

<script>
export default {
  props: ["players"],
  data() {
    return {
      teams: [],
      numberOfTeams: 2,
      numberOfPlayersPerTeam: 2,
    };
  },
  methods: {
    generateTeams() {
      let playersCopy = [...this.players];
      for (let i = 0; i < this.numberOfTeams; i++) {
        this.teams.push([]);
      }
      for (let i = 0; i < this.numberOfPlayersPerTeam; i++) {
        for (let j = 0; j < this.numberOfTeams; j++) {
          const randomIndex = Math.floor(Math.random() * playersCopy.length);
          this.teams[j].push(playersCopy[randomIndex]);
          playersCopy.splice(randomIndex, 1);
        }
        console.log("Players:");
        console.log(this.teams);
        console.log(this.players);
      }
      this.$emit("changePhase", 3);
    },
    back() {
      this.$emit("changePhase", 1);
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

h2 {
  text-decoration: underline;
}

.numberStyle {
  font-size: 64px;
}

.headerIcon {
  padding-left: 8px;
  font-size: 38px;
}
</style>
