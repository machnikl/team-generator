<template>
  <v-container class="mainContainer">
    <v-row class="playerContainer">
      <v-col cols="12">
        <v-row>
          <h1 class="ma-3">Team Picker</h1>
        </v-row>
      </v-col>
    </v-row>
    <v-row>
      <v-col cols="12">
        <h2 class="text-center">
          Hello! <br />
          Please add Players to generate Teams:
        </h2>
        <v-row class="justify-center">
          <v-col cols="auto" class="my-auto">
            <v-text-field
              label="Nickname"
              solo
              hide-details
              @keyup.enter.native="addPlayer"
              v-model="newPlayerName"
            ></v-text-field>
          </v-col>
          <v-col cols="auto">
            <v-btn class="mx-2 btnStyle" fab dark @click="addPlayer">
              <v-icon dark> mdi-plus </v-icon>
            </v-btn>
          </v-col>
        </v-row>
      </v-col>
    </v-row>
    <v-row>
      <v-col cols="12">
        <v-row>
          <Avatar v-for="player in players" :text="player" :key="player" />
        </v-row>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import Avatar from "@/components/Avatar";

export default {
  components: {
    Avatar,
  },
  data() {
    return {
      newPlayerName: "",
      players: [],
      teams: [],
      numberOfTeams: null,
      numberOfPlayersPerTeam: null,
    };
  },
  methods: {
    addPlayer() {
      let shortName = this.newPlayerName.substring(0, 3);
      this.players.push(shortName);
      this.newPlayerName = "";
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

.playerContainer {
  height: 30vh;
}

h1 {
  font-size: 1.2em;
}

h2 {
  font-size: 2em;
  margin-bottom: 28px;
}

h3 {
  font-size: 1.6em;
  color: white;
  margin-bottom: 14px;
}

.btnStyle {
  border: 3px solid white;
  background-color: transparent !important;
}
</style>
