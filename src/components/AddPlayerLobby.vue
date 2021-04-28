<template>
  <div class="outerContainer">
    <div style="height: 65vh">
      <v-row class="mb-2">
        <v-col cols="12">
          <h2 class="mb-2">Add Players:</h2>
          <v-row>
            <v-col cols="auto" class="my-auto">
              <v-text-field
                label="Nickname"
                solo
                hide-details
                @keyup.enter.native="addPlayer"
                v-model="newPlayerName"
              ></v-text-field>
            </v-col>
            <v-col cols="auto" class="my-auto">
              <v-btn
                class="mx-2 btnStyle"
                fab
                small
                dark
                :disabled="players.length > 7"
                @click="addPlayer"
              >
                <v-icon dark> mdi-plus </v-icon>
              </v-btn>
            </v-col>
          </v-row>
        </v-col>
      </v-row>
      <v-row class="bottomContainer">
        <v-col cols="12">
          <v-row>
            <v-img
              :src="require('../assets/team.svg')"
              class="mt-6"
              contain
              height="80"
            />
          </v-row>
          <v-row class="justify-center">
            <h3 v-if="players.length < 1">No players added...</h3>
            <Avatar
              v-for="player in players"
              :text="player"
              :key="player"
              class="mt-4"
            />
          </v-row>
        </v-col>
      </v-row>
    </div>
    <v-row justify="space-around" align-content="center">
      <v-col cols="auto">
        <v-btn @click="toTeamNumberChooser" :disabled="players.length < 2"
          >Generate Teams</v-btn
        >
      </v-col>
    </v-row>
  </div>
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
      numberOfTeams: 2,
      numberOfPlayersPerTeam: 2,
    };
  },
  methods: {
    addPlayer() {
      let shortName = this.newPlayerName.substring(0, 3);
      this.players.push(shortName);
      this.newPlayerName = "";
      this.$emit("newPlayer", shortName);
    },
    toTeamNumberChooser() {
      this.$emit("changePhase", 2);
    },
  },
};
</script>

<style scoped>
h2 {
  font-size: 21px;
  font-weight: bold;
  margin-bottom: 16px;
}

h3 {
  font-size: 18px;
  font-weight: bold;
}

.btnStyle {
  border: 3px solid white;
  background-color: transparent !important;
}

.bottomContainer {
  height: 75%;
  width: 100%;
  margin-left: auto;
  margin-right: auto;

  background-image: linear-gradient(to right, white 100%, white 100%),
    linear-gradient(to bottom, white 100%, white 100%),
    linear-gradient(to right, white 100%, white 100%),
    linear-gradient(to bottom, white 100%, white 100%);
  background-size: 100% 5px, 5px 100%, 100% 5px, 5px 100%;
  background-position: 0 0, 100% 0, 100% 100%, 0 100%;
  animation: bottomContainer 2.25s cubic-bezier(0.19, 1, 0.22, 1) 1;
  animation-play-state: running;
}

@keyframes bottomContainer {
  0% {
    background-size: 0 3px, 5px 0, 0 5px, 5px 0;
  }
  25% {
    background-size: 100% 5px, 5px 0, 0 5px, 5px 0;
  }
  50% {
    background-size: 100% 5px, 5px 100%, 0 5px, 5px 0;
  }
  75% {
    background-size: 100% 5px, 5px 100%, 100% 5px, 5px 0;
  }
  100% {
    background-size: 100% 5px, 5px 100%, 100% 5px, 5px 100%;
  }
}
</style>
