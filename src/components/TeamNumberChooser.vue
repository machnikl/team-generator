<template>
  <div>
    <h1 class="text-center">Teams Configurator</h1>
    <h2 class="text-center">How many teams?</h2>
    <div class="numberChooserContainer">
      <v-btn
        icon
        class="arrowStyle"
        @click="numberOfTeams--"
        :disabled="numberOfTeams < 3"
      >
        <v-icon color="white">mdi-minus-circle</v-icon>
      </v-btn>
      <span class="numberStyle pl-7"
        ><span>{{ numberOfTeams }}</span>
        <v-icon color="white" class="headerIcon"
          >mdi-account-group</v-icon
        ></span
      >
      <v-btn
        icon
        class="arrowStyle"
        @click="numberOfTeams++"
        :disabled="numberOfTeams > 3"
      >
        <v-icon color="white">mdi-plus-circle</v-icon>
      </v-btn>
    </div>
    <h2 class="text-center">Players per Team?</h2>
    <div class="numberChooserContainer">
      <v-btn
        icon
        class="arrowStyle"
        @click="numberOfPlayersPerTeam--"
        :disabled="numberOfPlayersPerTeam < 2"
      >
        <v-icon color="white">mdi-minus-circle</v-icon>
      </v-btn>
      <span class="numberStyle pl-7"
        ><span>{{ numberOfPlayersPerTeam }}</span>
        <v-icon color="white" class="headerIcon"
          >mdi-account-question</v-icon
        ></span
      >
      <v-btn
        icon
        class="arrowStyle"
        @click="numberOfPlayersPerTeam++"
        :disabled="numberOfPlayersPerTeam > 3"
      >
        <v-icon color="white">mdi-plus-circle</v-icon>
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
      this.$emit("generatedTeams", this.teams);
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
  font-size: 24px;
  position: relative;
  left: -11px;
  bottom: 40px;
}
</style>
