<template>
  <div v-if="showWon && this.mysteryPlayer" class="modal">
    <p style="font-size: 35px; margin: 2px">Well done!</p>
    <p>You guessed the mystery player in {{ 7 - this.turnsLeft }} {{ (7 - this.turnsLeft) > 1 ? 'turns' : 'turn' }}.</p>
    <p style="font-size: 20px; font-weight: bold">{{ this.mysteryPlayer.Player }}</p>
    <img style="object-fit: cover; max-height: 150px; margin-left: auto; margin-right: auto; margin-bottom: 10px; " :src="getImageSrc()" alt="" />

    <div id="gameResults" class="mini-wrapper" style="row-gap: 20px;" v-for="guess in guesses" v-bind:key="guess.id">
      <div :class="[conferenceCorrect(guess.CONF) ? 'correct' : 'incorrect', 'cell cell-border cell-border-top cell-spin-2']"></div>
      <div :class="[divisionCorrect(guess.DIV) ? 'correct' : divisionClose(guess.DIV) ? 'close' : 'incorrect', 'cell cell-border cell-border-top cell-spin-4']"></div>
      <div :class="[teamCorrect(guess.TEAM) ? 'correct' : 'incorrect', 'cell cell-border cell-border-top cell-spin-6']"></div>
      <div :class="[positionCorrect(guess.POS) ? 'correct' : positionClose(guess.POS) ? 'close' : 'incorrect', 'cell cell-border cell-border-top cell-spin-3']"></div>
      <div :class="[ageCorrect(guess.AGE) ? 'correct' : ageClose(guess.AGE) ? 'close' : 'incorrect', 'cell cell-border cell-border-top cell-spin-5']"></div>
    </div>
    <div id="gameResultsShared" v-for="guess in guesses" v-bind:key="guess.id">
    </div>

    <div style="margin-top: 1rem">Next Player in:</div>
    <div id="nextPlayerTime" style="font-size: 30px"></div>
    
    <div style="display: flex; flex-direction: row; margin-top: 1rem;">
      <button @click="copyToClipboard()" id="copybtn" class="button-43" role="button">Share</button>
      <button @click="closeShowWon()" class="button-43" role="button">Close</button>
    </div>
  </div>

  <div v-if="showLost && this.mysteryPlayer" class="modal">
    <p style="font-size: 20px">Better luck next time!</p>
    <p>The mystery player was:</p>
    <p style="font-size: 20px; font-weight: bold">{{ this.mysteryPlayer.Player }}</p>
    <img style="object-fit: cover; max-height: 150px; margin-left: auto; margin-right: auto; margin-bottom: 10px; " :src="getImageSrc()" alt="" />


    <div style="margin-top: 1rem">Next Player in:</div>
    <div id="nextPlayerTime" style="font-size: 30px"></div>

    <button @click="closeShowLost()" class="button-43" role="button">Close</button>
  </div>

  <div :class="[showWon || showLost ? 'modal-backdrop' : null, 'hello']">
    <h1>WADDLE</h1>
    <h2>A DAILY NFL PLAYER GUESSING GAME</h2>

    <div class="search">
      <input type="text" class="search-input" v-model="search" placeholder="Guess a player" :disabled="gameFinished || showWon || showLost || showHowToPlay" />
      <ul style="display: flex; flex-direction: column; border: 1px solid lightblue">
        <li class="search-result" v-for="player in filteredPlayers" v-bind:key="player.id" @click="guessPlayer(player.Player)">{{ player.Player}}</li>
      </ul>
    </div>

    <div v-if="this.mysteryPlayer" style="margin-top: 7rem; margin-bottom: 8rem;">
      <div :class="[this.turnsLeft > 6 ? 'hide' : 'wrapper']" style="row-gap: 20px;">
        <div class="title-cell"></div>
        <div class="title-cell">CONF</div>
        <div class="title-cell">DIV</div>
        <div class="title-cell">TEAM</div>
        <div class="title-cell">POS</div>
        <div class="title-cell">AGE</div>
      </div>
      <div class="wrapper" style="row-gap: 20px;" v-for="guess in guesses" v-bind:key="guess.id">
        <div class="cell cell-border name cell-border-top cell-spin-1">{{ guess.Player }}</div>
        <div :class="[conferenceCorrect(guess.CONF) ? 'correct' : 'incorrect', 'cell cell-border cell-border-top cell-spin-2']">
          <img style="height: 50px; width: 50px;" v-bind:src="require('../assets/conferences/' + guess.CONF + '.png')" />
        </div>
        <div :class="[divisionCorrect(guess.DIV) ? 'correct' : divisionClose(guess.DIV) ? 'close' : 'incorrect', 'cell cell-border cell-border-top cell-spin-4']">{{ guess.DIV }}</div>
        <div :class="[teamCorrect(guess.TEAM) ? 'correct' : 'incorrect', 'cell cell-border cell-border-top cell-spin-6']">
          <img style="height: 50px; width: 50px;" v-bind:src="require('../assets/teams/' + guess.TEAM + '.png')" />
        </div>
        <div :class="[positionCorrect(guess.POS) ? 'correct' : positionClose(guess.POS) ? 'close' : 'incorrect', 'cell cell-border cell-border-top cell-spin-3']">{{ guess.POS }}</div>
        <div :class="[ageCorrect(guess.AGE) ? 'correct' : ageClose(guess.AGE) ? 'close' : 'incorrect', 'cell cell-border-top cell-spin-5']" style="flex-direction: row">
          {{ guess.AGE }}
          <svg v-if="guess.AGE > this.mysteryPlayer.AGE" xmlns="http://www.w3.org/2000/svg" class="h-3 w-3" style="height: 25px" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
            <path stroke-linecap="round" stroke-linejoin="round" d="M17 13l-5 5m0 0l-5-5m5 5V6" />
          </svg>
          <svg v-if="guess.AGE < this.mysteryPlayer.AGE" xmlns="http://www.w3.org/2000/svg" class="h-3 w-3" style="height: 25px" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
            <path stroke-linecap="round" stroke-linejoin="round" d="M7 11l5-5m0 0l5 5m-5-5v12" />
          </svg>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import moment from 'moment'

export default {
  name: 'PlayGame',
  props: {
    msg: String,
    showHowToPlay: Boolean
  },
  data() {
    return {
      search: '',
      turnsLeft: 7,
      mysteryPlayer: null,
      playerDatabase: null,
      guesses: [],
      showInstructions: false,
      showWon: false,
      showLost: false,
      gameFinished: false
    }
  },
  created() {
    const response = fetch("https://docs.google.com/spreadsheets/d/e/2PACX-1vSu63wW64Ku7O7A36x9Sr8TWBdpAsdsKAWBoaiK7ndsrCkHerxIIcyuiKemsjyIlQ/pub?gid=1468918379&single=true&output=csv", {
      method: 'get',
      headers: {
        'content-type': 'text/csv;charset=UTF-8'
      }
    }).then((response) => response.text())
    .then((text) => {
      return this.csvToArray(text)
    })

    const getPlayerDatabase = () => {
      response.then((response) => {
        window.data = response;
        this.playerDatabase = response
      })
    }
    
    getPlayerDatabase()

    const $this = this;

    // new player per day
    function waitForDatabase() {
      if ($this.playerDatabase != null) {
        const ms_per_day = 24 * 60 * 60 * 1000
        let days_since_epoch = Math.floor((new Date()).getTime() / ms_per_day)
        let player_index = days_since_epoch % $this.playerDatabase.length
        $this.mysteryPlayer = $this.playerDatabase[player_index]
    
      } else {
        setTimeout(waitForDatabase, 150)
      }
    }

    waitForDatabase()
    // fill current day guesses if present
    let guesses = this.$store.getters.getGuesses
    if (guesses) {
      guesses.forEach(guess => {
        this.guesses.push(guess)
        this.turnsLeft -= 1
      })
    }
    // show hours result if already played
    let results = this.$store.getters.getResultsHistoryForTimePeriod
    if (results != null) {
      if (results.won) {
        this.showWon = true;
      } else {
        this.showLost = true
      }
      this.gameFinished = true
    }

    setInterval(function() {
        if ($this.showHowToPlay) {
          $this.showWon = false
          $this.showLost = false
        }

      let eventTime = moment().endOf('day')
      const timeLeft = moment.utc(eventTime.diff(moment())); // get difference between now and timestamp
      const formatted = timeLeft.format('HH:mm:ss'); // make pretty

      let el = document.getElementById("nextPlayerTime")
      if (el) {
        el.innerHTML = formatted
      }
    }, 1000)
  },
  computed: {
    filteredPlayers() {
      if (this.search == "") {
        return []
      }
      var diacritics = {
        a: 'ÀÁÂÃÄÅàáâãäåĀāąĄ',
        c: 'ÇçćĆčČ',
        d: 'đĐďĎ',
        e: 'ÈÉÊËèéêëěĚĒēęĘ',
        i: 'ÌÍÎÏìíîïĪī',
        l: 'łŁ',
        n: 'ÑñňŇńŃ',
        o: 'ÒÓÔÕÕÖØòóôõöøŌō',
        r: 'řŘ',
        s: 'ŠšśŚ',
        t: 'ťŤ',
        u: 'ÙÚÛÜùúûüůŮŪū',
        y: 'ŸÿýÝ',
        z: 'ŽžżŻźŹ'
      }

      function replaceDiacritics(text) { return text .split('') .map(l => Object.keys(diacritics).find(k => diacritics[k].includes(l)) || l) .join(''); }
      let players = this.playerDatabase.filter(player => {
        return replaceDiacritics(player.Player.toLowerCase().normalize('NFD').replace(/[\u0300-\u036f]/g, "")).includes(this.search.toLowerCase())
      })

      return players.slice(0, 5)
    }
  },
  methods: {
      csvToArray(str, delimiter = ",") {
        // slice from start of text to the first \n index
        // use split to create an array from string by delimiter
        const headers = str.slice(0, str.indexOf("\n")).split(delimiter);

        // slice from \n index + 1 to the end of the text
        // use split to create an array of each csv value row
        const rows = str.slice(str.indexOf("\n") + 1).split("\n");

        // Map the rows
        // split values from each row into an array
        // use headers.reduce to create an object
        // object properties derived from headers:values
        // the object passed as an element of the array
        const arr = rows.map(function (row) {
          const values = row.split(delimiter);
          const el = headers.reduce(function (object, header, index) {
            object[header] = values[index];
            return object;
          }, {});
          return el;
        });

        // return the array
        return arr;
    },
    guessPlayer(guessedName) {
      let player = this.playerDatabase.find(player => 
        player.Player.toLowerCase() == guessedName.toLowerCase()
      )
      this.guesses.push(player)
      this.$store.commit('addGuess', player)
      this.search = ''
      this.turnsLeft -= 1
      if (player.Player == this.mysteryPlayer.Player) {
        const $this = this;
        setTimeout(function() {
          $this.showWon = true
          $this.gameFinished = true
          $this.$store.commit("saveResult", {turnsTaken: (7 - $this.turnsLeft), won: true})
        }, 1000)
      } else if (this.turnsLeft == 0) {
        this.showLost = true
        this.$store.commit("saveResult", {turnsTaken: 7, won: false})
      }
    },
    conferenceCorrect(conferenceGuess) {
      return conferenceGuess == this.mysteryPlayer.CONF
    },
    divisionCorrect(divisionGuess) {
      return divisionGuess == this.mysteryPlayer.DIV
    },
    divisionClose(divisionGuess) {
      return this.mysteryPlayer.CONF == divisionGuess.split(" ")[0]
    },
    teamCorrect(teamGuess) {
      return teamGuess == this.mysteryPlayer.TEAM
    },
    positionCorrect(positionGuess) {
      return positionGuess == this.mysteryPlayer.POS
    },
    positionClose(positionGuess) {
      let offense = ["WR", "RB", "TE", "QB", "K"]
      let defense = ["LB", "DL", "DB"]
      let position = this.mysteryPlayer.POS
      if(offense.includes(position)) {
        return offense.includes(positionGuess)
      } else if (defense.includes(position)) {
        return defense.includes(positionGuess)
      }
    },
    ageCorrect(ageGuess) {
      return ageGuess == this.mysteryPlayer.AGE
    },
    ageClose(ageGuess) {
      let closeArray = []
      let cAge = Number(this.mysteryPlayer.AGE)
      for (let i = cAge - 2; i <= cAge + 2; i++) {
        closeArray.push(i)
      }
      return closeArray.includes(Number(ageGuess))
    },
    closeShowWon() {
      this.showWon = false
    },
    closeShowLost() {
      this.showLost = false
    },
    getImageSrc() {
      return "https://drive.google.com/uc?export=view&id=" + this.mysteryPlayer.image
    },
    copyToClipboard() {
      const ms_per_day = 24 * 60 * 60 * 1000
      let days_since_epoch = Math.floor((new Date()).getTime() / ms_per_day)
      let str = `Waddle ${days_since_epoch - 19071} ${7-this.turnsLeft}/7 \n\n`
      var guesses = this.guesses
      // let results = document.getElementById("gameResults")
      for(var i = 0; i<this.guesses.length; i++) {
        if (this.conferenceCorrect(guesses[i].CONF)) {
          str += "🟩" 
        } else {
          str += "⬜"
        }
        if (this.divisionCorrect(guesses[i].DIV)) {
          str += "🟩" 
        } else if (this.divisionClose(guesses[i].DIV)) {
          str += "🟨"
        } else {
          str += "⬜"
        }
        if (this.teamCorrect(guesses[i].TEAM)) {
          str += "🟩"
        } else {
          str += "⬜"
        }
        if (this.positionCorrect(guesses[i].POS)) {
          str += "🟩"
        } else if (this.positionClose(guesses[i].POS)) {
          str += "🟨"
        } else {
          str += "⬜"
        }
        if (this.ageCorrect(guesses[i].AGE)) {
          str += "🟩"
        } else if (this.ageClose(guesses[i].AGE)) {
          str += "🟨"
        } else {
          str += "⬜"
        }
        str += "\n"
      }

      str += "\n\nPlay here:\n"
      str += "https://www.playwaddle.com"


      function copyRichText(text) {
        const listener = function(ev) {
          ev.preventDefault();
          ev.clipboardData.setData('text/html', text);
          ev.clipboardData.setData('text/plain', text);
        };
        document.addEventListener('copy', listener);
        document.execCommand('copy');
        document.removeEventListener('copy', listener);
      }

      if (str) {
        let result;
        let textarea;
        try {
          textarea = document.createElement('textarea');
          textarea.setAttribute('readonly', true);
          textarea.setAttribute('contenteditable', true);
          textarea.style.position = 'fixed'; // prevent scroll from jumping to the bottom when focus is set.
          textarea.value = str;

          document.body.appendChild(textarea);

          textarea.focus();
          textarea.select();

          const range = document.createRange();
          range.selectNodeContents(textarea);

          const sel = window.getSelection();
          sel.removeAllRanges();
          sel.addRange(range);

          textarea.setSelectionRange(0, textarea.value.length);
          result = document.execCommand('copy');
        } catch (err) {
          console.error(err);
          result = null;
        } finally {
          document.body.removeChild(textarea);
          document.getElementById('copybtn').innerHTML = "Copied!"
        }
        // manual copy fallback using prompt
        if (!result) {
          const isMac = navigator.platform.toUpperCase().indexOf('MAC') >= 0;
          const copyHotkey = isMac ? '⌘C' : 'CTRL+C';
          result = prompt(`Press ${copyHotkey}`, str); // eslint-disable-line no-alert
          if (!result) {
            return false;
          }
        }
        return true;
      } else {
        copyRichText(str);
        document.getElementById('copybtn').innerHTML = "Copied!"
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1 {
  font-weight: 'bold';
  color: #288708;
  font-size: 30px;
  margin-bottom: 1rem;
}
@media only screen and (min-width: 600px) {
  h1 {
    font-size: 40px;
  }
}
@media only screen and (min-width: 1000px) {
  h1 {
    font-size: 50px;
  }
}
h2 {
  font-size: 14px;
}
@media only screen and (min-width: 600px) {
  h2 {
    font-size: 18px;
  }
}
@media only screen and (min-width: 1000px) {
  h2 {
    font-size: 20px;
  }
}
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
}
li:hover {
  background: #DEF2F1;
}
a {
  color: #42b983;
}
.hide {
  display: none;
}
.modal {
  display: flex;
  justify-content: center;
  z-index: 50;
  padding: 3rem;
  border-radius: 25px;
  position: absolute; 
  left: 0;
  right: 0; 
  margin-left: auto; 
  margin-right: auto; 
  min-width: 240px;
  max-width: 480px; 
  margin-bottom: 5rem;
  top: 10rem; 
  border: 1px solid lightblue; 
  background: #fff
}
.modal-backdrop {
  opacity: 0.5 !important;
}
.search-input {
  max-width: 480px;
  min-width: 80px;
  padding: 1rem; 
  font-size: 20px; 
  position: relative; 
  margin-right: auto;
  margin-left: auto;
}
.search {
  position: absolute; 
  left: 0; 
  right: 0; 
  margin-left: auto; 
  margin-right: auto; 
  max-width: 480px;
  min-width: 80px;
  margin-bottom: 5rem;
}
.search-result {
  cursor: pointer; 
  z-index: 50; 
  position: relative; 
  background: white; 
  min-width: 340px;
  max-width: 100%;
  padding: 1rem;
}
.name {
  background: #DEF2F1;
}
.wrapper {
  display: grid;
  width: 100%;
  grid-template-columns: repeat(auto-fit, minmax(40px, 1fr));
  grid-auto-rows: minmax(55px, auto);
}
@media only screen and (min-width: 600px) {
  .wrapper {
    margin: auto;
    width: 80%;
  }
}
@media only screen and (min-width: 1000px) {
  .wrapper {
    margin: auto;
    width: 60%;
  }
}

.mini-wrapper {
  justify-content: center;
  margin-inline: auto;
  display: grid;
  width: 50%;
  grid-template-columns: repeat(5, 1fr);
  grid-auto-rows: minmax(15px, auto);
}
@keyframes spin { 
    from { 
        transform: rotateY(180deg); 
    } to { 
        transform: rotateY(360deg); 
    }
}
.cell {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding-inline: 1.5rem;
  padding: 1rem;
  font-size: 12px;
}
@media only screen and (min-width: 600px) {
  .cell {
    font-size: 16px;
  }
}
@media only screen and (min-width: 1000px) {
  .cell {
    font-size: 21px;
  }
}
.cell-spin-1 {
  animation: spin .2s linear;
}
.cell-spin-2 {
  animation: spin .4s linear;
}
.cell-spin-3 {
  animation: spin .6s linear;
}
.cell-spin-4 {
  animation: spin .8s linear;
}
.cell-spin-5 {
  animation: spin 1s linear;
}
.cell-spin-6 {
  animation: spin 1.2s linear;
}
.title-cell {
  margin-top: 2rem;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 2vmin;
}
.cell-border-top {
  border-top: 2px solid #fff;
}
@media only screen and (min-width: 600px) {
  .cell-border-top {
    border-top: 4px solid #fff;
  }
}
.cell-border {
  border-right: 2px solid #fff;
}
@media only screen and (min-width: 600px) {
  .cell-border {
    border-right: 4px solid #fff;
  }
}
.correct {
  background: #37be75;
  color: #FEFFFF
}
.incorrect {
  background: #878a8c;
  color: #FEFFFF
}
.close {
  background: #fad91e;
  color: #FEFFFF
}
</style>
