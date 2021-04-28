<template>
  <v-container class="mainContainer">
    <v-row class="playerContainer">
      <v-col cols="12">
        <v-row>
          <h1 class="ma-3">Team Picker</h1>
        </v-row>
        <v-row>
          <Avatar v-for="player in players" :text="player" :key="player" />
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
            <v-text-field label="Max" solo hide-details></v-text-field>
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
      <v-col cols="12"></v-col>
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
      players: ["NIK", "ANN", "KAT", "SEB", "FLO"],
      teams: [],
      numberOfTeams: null,
      numberOfPlayersPerTeam: null,
    };
  },
};
</script>

<style scoped>
.mainContainer {
  min-height: 100vh;
  background: linear-gradient(0deg, #7474bf 0%, #348ac7 100%);
  color: white;
}

.playerContainer {
  height: 30vh;
}

h1 {
  font-size: 1.4em;
}

h2 {
  font-size: 2em;
  margin-bottom: 28px;
}

.btnStyle {
  border: 3px solid white;
  background-color: transparent !important;
}
</style>
