<template>
  <v-container class="mainContainer">
    <LogoContainer />
    <transition name="slide-fade" mode="out-in">
      <div v-if="phase === 1" key="phase1">
        <AddPlayerLobby @newPlayer="newPlayerAdded" />
        <v-row justify="center" class="mt-8">
          <v-btn @click="generateTeams" :disabled="players.length < 2"
            >Generate Teams</v-btn
          >
        </v-row>
      </div>
      <div v-if="phase === 2" key="phase2">
        <TeamNumberChooser />
      </div>
    </transition>
  </v-container>
</template>

<script>
import LogoContainer from "@/components/LogoContainer";
import AddPlayerLobby from "@/components/AddPlayerLobby";
import TeamNumberChooser from "@/components/TeamNumberChooser";

export default {
  components: {
    LogoContainer,
    AddPlayerLobby,
    TeamNumberChooser,
  },
  data() {
    return {
      phase: 1,
      players: [],
      teams: [],
      numberOfTeams: 2,
      numberOfPlayersPerTeam: 2,
    };
  },
  methods: {
    newPlayerAdded(newPlayer) {
      this.players.push(newPlayer);
      console.log(this.players);
    },
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
      this.phase = 2;
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
  min-height: 100vh;
  background: linear-gradient(132deg, #fc415a, #591bc5, #212335);
  background-size: 400% 400%;
  animation: Gradient 15s ease infinite;
  position: relative;
  height: 100vh;
  width: 100%;
  overflow: hidden;
  color: white;
}

.slide-fade-enter-active {
  transition: all 0.3s ease;
}
.slide-fade-leave-active {
  transition: all 0.3s cubic-bezier(1, 0.5, 0.8, 1);
}
.slide-fade-enter {
  transform: translateX(40px);
  opacity: 0;
}

.slide-fade-leave-to
  /* .slide-fade-leave-active below version 2.1.8 */ {
  transform: translateX(-40px);
  opacity: 0;
}
</style>
