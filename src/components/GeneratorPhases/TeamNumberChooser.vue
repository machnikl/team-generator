<template>
  <div class="outerContainer">
    <div>
      <h1 class="text-center">Teams Configurator</h1>
      <h2 class="text-center">How many teams?</h2>
      <NumberChooser
        @valueChange="valueChangeTeamNr"
        iconName="mdi-account-group"
      />
      <h2 class="text-center">Players per Team?</h2>
      <NumberChooser
        @valueChange="valueChangePlayerNr"
        iconName="mdi-account"
      />
    </div>
    <v-row justify="space-around" align-content="center">
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
import NumberChooser from "@/components/General/NumberChooser";

export default {
  components: {
    NumberChooser,
  },
  props: {
    players: Array,
  },
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
      }
      this.$emit("generatedTeams", this.teams);
    },
    back() {
      this.players.length = 0;
      this.$emit("changePhase", 1);
    },
    valueChangeTeamNr(value) {
      this.numberOfTeams = value;
    },
    valueChangePlayerNr(value) {
      this.numberOfPlayersPerTeam = value;
    },
  },
};
</script>

<style scoped>
h2 {
  text-decoration: underline;
}
</style>
