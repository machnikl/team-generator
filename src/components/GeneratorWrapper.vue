<template>
  <v-container class="mainContainer">
    <LogoContainer />
    <transition name="slide-fade" mode="out-in">
      <div v-if="phase === 1" key="phase1">
        <AddPlayerLobby @newPlayer="newPlayerAdded" />
        <v-row justify="center" class="mt-8">
          <v-btn @click="toTeamNumberChooser" :disabled="players.length < 2"
            >Generate Teams</v-btn
          >
        </v-row>
      </div>
      <div v-if="phase === 2" key="phase2">
        <TeamNumberChooser
          :players="players"
          @changePhase="changePhase"
          @generatedTeams="generatedTeams"
        />
      </div>
      <div v-if="phase === 3" key="phase3">
        <PlayerSelectionDisplay @changePhase="changePhase" :teams="teams" />
      </div>
    </transition>
  </v-container>
</template>

<script>
import LogoContainer from "@/components/LogoContainer";
import AddPlayerLobby from "@/components/AddPlayerLobby";
import TeamNumberChooser from "@/components/TeamNumberChooser";
import PlayerSelectionDisplay from "@/components/PlayerSelectionDisplay";

export default {
  components: {
    LogoContainer,
    AddPlayerLobby,
    TeamNumberChooser,
    PlayerSelectionDisplay,
  },
  data() {
    return {
      phase: 1,
      players: [],
      teams: [],
    };
  },
  methods: {
    newPlayerAdded(newPlayer) {
      this.players.push(newPlayer);
      console.log(this.players);
    },
    toTeamNumberChooser() {
      this.phase = 2;
    },
    changePhase(phase) {
      this.phase = phase;
    },
    generatedTeams(teams) {
      this.teams = teams;
      this.phase = 3;
    },
  },
};
</script>

<style scoped>
@keyframes Gradient {
  0% {
    background-position: 0% 50%;
  }
  50% {
    background-position: 100% 50%;
  }
  100% {
    background-position: 0% 50%;
  }
}

.mainContainer {
  min-height: 100%;
  background: linear-gradient(132deg, #fc415a, #591bc5, #212335);
  background-size: 400% 400%;
  animation: Gradient 15s ease infinite;
  position: relative;
  height: 100%;
  width: 100vw;
  box-sizing: border-box;
  overflow-x: hidden;
  overflow-y: hidden;
  color: white;
}
</style>
