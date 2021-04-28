<template>
  <v-container class="mainContainer">
    <v-row class="logoContainer">
      <v-col cols="12">
        <v-img
          :src="require('../assets/logo2.svg')"
          class="mt-6"
          contain
          height="80"
        />
      </v-col>
    </v-row>
    <v-row class="mb-8">
      <v-col cols="12">
        <h2 class="text-center">Add Players:</h2>
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
          <v-col cols="auto" class="my-auto">
            <v-btn class="mx-2 btnStyle" fab small dark @click="addPlayer">
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
        <v-row>
          <Avatar v-for="player in players" :text="player" :key="player" />
        </v-row>
      </v-col>
    </v-row>
    <v-row v-if="players.length > 0" justify="center" class="mt-10">
      <v-btn @click="generateTeams">Generate Teams</v-btn>
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
      numberOfTeams: 2,
      numberOfPlayersPerTeam: 2,
    };
  },
  methods: {
    addPlayer() {
      let shortName = this.newPlayerName.substring(0, 3);
      this.players.push(shortName);
      this.newPlayerName = "";
    },
    generateTeams() {
      for (let i = 0; i < this.numberOfTeams; i++) {
        this.teams.push([]);
      }
      for (let i = 0; i < this.numberOfPlayersPerTeam; i++) {
        for (let j = 0; j < this.numberOfTeams; j++) {
          const randomIndex = Math.floor(Math.random() * this.players.length);
          this.teams[j].push(this.players[randomIndex]);
          this.players.splice(randomIndex, 1);
        }
        console.log("Players:");
        console.log(this.teams);
      }
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

.logoContainer {
  height: 22vh;
}

h1 {
  font-size: 1.2em;
}

h2 {
  font-size: 2em;
  font-weight: normal;
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

.bottomContainer {
  height: 40vh;
  margin-left: 5px;
  margin-right: 5px;

  background-image: linear-gradient(to right, white 100%, white 100%),
    linear-gradient(to bottom, white 100%, white 100%),
    linear-gradient(to right, white 100%, white 100%),
    linear-gradient(to bottom, white 100%, white 100%);
  background-size: 100% 5px, 5px 100%, 100% 5px, 5px 100%;
  background-position: 0 0, 100% 0, 100% 100%, 0 100%;
  animation: bg 2.25s cubic-bezier(0.19, 1, 0.22, 1) 1;
  animation-play-state: running;
}

@keyframes bg {
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

div {
}
</style>
