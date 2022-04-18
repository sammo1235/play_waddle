<template>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Roboto+Slab&family=Roboto:wght@100;300&display=swap" rel="stylesheet"> 

  <div class="header">
    <div style="flex-direction: row; display: flex; margin-right: auto; margin-left: auto; padding: 1rem;">
      <div @click="showAboutModal()" style="display: flex; align-items: center; margin-left: auto; cursor: pointer;">
        <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="#2c3e50" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><circle cx="12" cy="12" r="10"></circle><line x1="12" y1="16" x2="12" y2="12"></line><line x1="12" y1="8" x2="12.01" y2="8"></line></svg>
      </div>
      <div @click="showStatsModal()" style="display: flex; align-items: center; margin-left: 2rem; cursor: pointer;">
        <svg style="margin-left: 6px;" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="#2c3e50" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M20.2 7.8l-7.7 7.7-4-4-5.7 5.7"/><path d="M15 7h6v6"/></svg>
      </div>
      <div @click="showHowTo()" style="display: flex; align-items: center; margin-left: 2rem; cursor: pointer;">
        <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="#2c3e50" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><circle cx="12" cy="12" r="10"></circle><path d="M9.09 9a3 3 0 0 1 5.83 1c0 2-3 3-3 3"></path><line x1="12" y1="17" x2="12.01" y2="17"></line></svg>
      </div>
      <div @click="showSupportModal()" style="display: flex; align-items: center; margin-left: 2rem; cursor: pointer;">
        <svg style="margin-left: 6px;" xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="#2c3e50" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M20.84 4.61a5.5 5.5 0 0 0-7.78 0L12 5.67l-1.06-1.06a5.5 5.5 0 0 0-7.78 7.78l1.06 1.06L12 21.23l7.78-7.78 1.06-1.06a5.5 5.5 0 0 0 0-7.78z"></path></svg>
      </div>
      <div style="display: flex; align-items: center; margin-left: 2rem; margin-right: auto; cursor: pointer;">
          <a target="_blank" href="https://twitter.com/playwaddle" style="align-items: center">
            <img style="height: 38px; margin-top: 4px" v-bind:src="require('./assets/twitter.png')" />
          </a>
      </div>
    </div>
  </div>

  <div v-if="showHowToPlay" class="modal">
    <p style="font-size: 25px">How to play</p>
    <p>You get 7 guesses to identify the mystery NFL player!</p>
    <p><span style="color: #37be75">GREEN:</span> In any field means that you guessed the corresponding attribute correctly.</p>
    <p><span style="color: #ffa64d">YELLOW:</span> In the division field means that the mystery player plays in that conference, but in a different division.</p>
    <p><span style="color: #ffa64d">YELLOW:</span> In the position field means that the mystery player does play on that side of the ball, but at a different position.</p>
    <p><span style="color: #ffa64d">YELLOW:</span> In the age field means that you guessed within 2 years of the mystery player's age.</p>
    <p>Enjoy a new mystery player every day!</p>
    <p>Copyright 2022. All Rights Reserved.</p>
    <button @click="showHowTo()" class="button-43" role="button">Close</button>
  </div>

  <div v-if="showAbout" class="modal">
    <p style="font-size: 25px">About Waddle:</p>
    <p>Each mystery player is semi-randomly picked from the top fantasy football players (including IDPs).</p>
    <p>Much love and all relevant rights to everyone featured.</p>
    <p>The player pool includes the following positions:</p>
    <p>Offense: QB, RB, WR, TE, K</p>
    <p>Defense: DL, LB, DB</p>
    <p>A special shout out to <a target="_blank" href="https://www.nytimes.com/games/wordle/index.html">Wordle</a>, who put down the first idea lego.</p>
    <p>Enjoy! 👊</p>
    <a target="_blank" href="https://docs.google.com/document/d/10QWWaZ9N590j0_J2_FIdfdIX5pQO4Wmskud4_C5bk3w/edit?usp=sharing">Privacy Policy</a>
    <button @click="showAboutModal()" class="button-43" role="button">Close</button>
  </div>

  <div v-if="showSupport" class="modal">
    <p style="font-size: 25px">Support</p>
    <p>If you've enjoyed playing Waddle, please consider supporting the
    <a target="_blank" href="https://donate.redcrossredcrescent.org/ua/donate/~my-donation">Ukranian Red Cross</a>
    . Any amount will help and they could use the support right now. Thank you! 🙏</p>
    <button @click="showSupportModal()" class="button-43" role="button">Close</button>
  </div>

  <div v-if="showStats" class="modal">
    <p style="font-size: 35px;">Statistics</p>
    <div style="display: flex; justifyContent: space-evenly;">
      <div style="display: flex; flex-direction: column">
        <p style="font-size: 30px; margin: 0px;">{{ totalGamesPlayed }}</p>
        <p>Played</p>
      </div>
      <div style="display: flex; flex-direction: column">
        <p style="font-size: 30px; margin: 0px;">{{ totalGamesWon }}</p>
        <p>Won</p>
      </div>
      <div style="display: flex; flex-direction: column">
        <p style="font-size: 30px; margin: 0px;">{{ winRatePercentage }}%</p>
        <p>Win Rate</p>
      </div>
    </div>
    <p>Guess Distribution:</p>
    <div style="display: flex; flex-direction: column-reverse; justifyContent: space-evenly; margin: 0px; align-items: flex-start; padding-inline: 1rem;">
      <div style="display: flex; width: 100%">
        <p style="margin: 5px">7</p><p class="progress-bar" :style="{'width': guessedInPercentage(7)}"><span style="margin-right: 4px;">{{ guessedIn(7) }}</span></p>
      </div>
      <div style="display: flex; width: 100%">
        <p style="margin: 5px">6</p><p class="progress-bar" :style="{'width': guessedInPercentage(6)}"><span style="margin-right: 4px;">{{ guessedIn(6) }}</span></p>
      </div>
      <div style="display: flex; width: 100%">
        <p style="margin: 5px">5</p><p class="progress-bar" :style="{'width': guessedInPercentage(5)}"><span style="margin-right: 4px;">{{ guessedIn(5) }}</span></p>
      </div>
      <div style="display: flex; width: 100%">
        <p style="margin: 5px">4</p><p class="progress-bar" :style="{'width': guessedInPercentage(4)}"><span style="margin-right: 4px;">{{ guessedIn(4) }}</span></p>
      </div>
      <div style="display: flex; width: 100%">
        <p style="margin: 5px">3</p><p class="progress-bar" :style="{'width': guessedInPercentage(3)}"><span style="margin-right: 4px;">{{ guessedIn(3) }}</span></p>
      </div>
      <div style="display: flex; width: 100%">
        <p style="margin: 5px">2</p><p class="progress-bar" :style="{'width': guessedInPercentage(2)}"><span style="margin-right: 4px;">{{ guessedIn(2) }}</span></p>
      </div>
      <div style="display: flex; width: 100%">
        <p style="margin: 5px; margin-right: 8px;">1</p><p class="progress-bar" :style="{'width': guessedInPercentage(1)}"><span style="margin-right: 4px;">{{ guessedIn(1) }}</span></p>
      </div>
    </div>
    <button @click="showStatsModal()" class="button-43" role="button">Close</button>
  </div>

  <div :class="[showHowToPlay || showStats ? 'modal-backdrop' : null, 'hello']">
    <Game :show-how-to-play="this.showHowToPlay || this.showStats || this.showAbout || this.showSupport" />
  </div>
</template>

<script>
import Game from './components/Game.vue'
export default {
  name: 'App',
  components: {
    Game
  },
  data() {
    return {
      showHowToPlay: false,
      showStats: false,
      showAbout: false,
      showSupport: false,
    }
  },
  created() {
    if(!this.$store.getters.hasSeenTutorial) {
      this.showHowToPlay = true
      this.$store.commit('seenTutorial')
    }
    // Title
    document.title = "Waddle"

    // twitter script
    let Script = document.createElement("script");
    Script.setAttribute("src", "https://platform.twitter.com/widgets.js");
    document.body.appendChild(Script);
  },
  computed: {
    totalGamesPlayed() {
      return Object.keys(this.$store.getters.getResultsHistory).length;
    },
    totalGamesWon() {
      let results = this.$store.getters.getResultsHistory
      return Object.keys(results).filter((key) => results[key].won).length
    },
    winRatePercentage() {
      let results = this.$store.getters.getResultsHistory
      if (Object.keys(results).length == 0) {
        return 0
      } else {
        return Math.round((Object.keys(results).filter((key) => results[key].won).length / Object.keys(results).length) * 100)
      }
    }
  },
  methods: {
    showHowTo() {
      this.showStats = false;
      this.showAbout = false;
      this.showSupport = false;
      this.showHowToPlay = !this.showHowToPlay
    },
    showStatsModal() {
      this.showHowToPlay = false
      this.showAbout = false;
      this.showSupport = false;
      this.showStats = !this.showStats
    },
    showAboutModal() {
      this.showStats = false;
      this.showHowToPlay = false;
      this.showSupport = false;
      this.showAbout = !this.showAbout
    },
    showSupportModal() {
      this.showStats = false;
      this.showHowToPlay = false;
      this.showAbout = false;
      this.showSupport = !this.showSupport
    },
    guessedIn(turnsTaken) {
      let results = this.$store.getters.getResultsHistory   
      return Object.keys(results).filter((key) => results[key].turns_taken == turnsTaken).length
    },
    guessedInPercentage(turnsTaken) {
      let results = this.$store.getters.getResultsHistory
      if (this.totalGamesWon2() > 0) {
        let wonInTurnsTaken = Object.keys(results).filter((key) => results[key].turns_taken == turnsTaken).length
        if (wonInTurnsTaken == 0) {
          return "5%"
        } else {
          let guessedInPerc = Object.keys(results).filter((key) => results[key].turns_taken == turnsTaken).length / this.totalGamesWon2()
          if (guessedInPerc < 0.05) {
            return "5%"
          } else {
            return `${guessedInPerc * 100}%`
          }
        }
      } else {
        return "5%"
      }
    },
    totalGamesWon2() {
      let results = this.$store.getters.getResultsHistory
      return Object.keys(results).filter((key) => results[key].won).length
    },
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Roboto+Slab&family=Roboto:wght@100;300&display=swap');
@font-face {
  font-family: "Roboto Slab";
}
#app {
  font-family: "Roboto Slab";
  text-align: center;
  color: #2c3e50;
}
a {
  color: #288708;
}
a:visited {
  color: #288900;
}
h3 {
  font-size: 12px;
}
@media only screen and (min-width: 600px) {
  h3 {
    font-size: 18px;
  }
}
@media only screen and (min-width: 1000px) {
  h3 {
    font-size: 20px;
  }
}
svg {
  width: 16px;
  height: 16px;
}
@media only screen and (min-width: 600px) {
  svg {
    width: 20px;
    height: 20px;
  }
}
@media only screen and (min-width: 1000px) {
  svg {
    width: 25px;
    height: 25px;
  }
}
.modal-backdrop {
  opacity: 0.5 !important;
}
.modal {
  display: flex;
  flex-direction: column;
  z-index: 50;
  padding: 3rem;
  border-radius: 25px;
  position: absolute; 
  left: 0;
  right: 0; 
  margin-left: auto; 
  margin-right: auto; 
  min-width: 240px;
  max-width: 480px; /* Need a specific value to work */
  margin-bottom: 5rem;
  top: 6rem; 
  border: 1px solid lightblue; 
  background: #fff;
  box-shadow: 5px 10px;
}
.header {
  width: 100%;
  background: #fff;
  border: 1px solid black;
  opacity: 50;
}
.footer {
  position: fixed;
  bottom: 0;
  width: 100%;
  background: #3AAFA9;
}
@media only screen and (min-width: 600px) {
  .footer {
    margin-top: 2rem;
    height: 4rem;
  }
}
body {
  margin: 0;
}
.progress-bar {
  font-size: 14px;
  display: inline-block; 
  margin: 3px; 
  padding: 0.2rem; 
  background: #878a8c; 
  color: #fff;
  text-align: right
}
/* CSS */
.button-43 {
  background-image: linear-gradient(-180deg, #37AEE2 0%, #1E96C8 100%);
  border-radius: .5rem;
  box-sizing: border-box;
  color: #FFFFFF;
  display: flex;
  font-size: 16px;
  margin-top: 1rem;
  margin-right: auto;
  margin-left: auto;
  justify-self: center;
  justify-content: center;
  padding: 1rem 1.75rem;
  text-decoration: none;
  border: 0;
  cursor: pointer;
  user-select: none;
  -webkit-user-select: none;
  touch-action: manipulation;
}

.button-43:hover {
  background-image: linear-gradient(-180deg, #1D95C9 0%, #17759C 100%);
}

@media (min-width: 768px) {
  .button-43 {
    padding: 1rem 2rem;
  }
}
</style>
