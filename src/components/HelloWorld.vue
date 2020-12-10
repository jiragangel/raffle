<template>
  <div v-if="!showWinners" class="main">
    <div class="header">
      <button class="toggle-entries" @click="hideEntries = !hideEntries">X</button>
    </div>
    <div class="content">
      <div class="entries" :class="{
        'd-none': hideEntries
      }">
        <textarea v-model="entriesText" @input="updateEntries" />
      </div>
      <div class="raffle-main" :class="{
        'w-100': hideEntries
      }">
        <h1>
          {{ winner.name }}
        </h1>
        <h2>
          {{ winner.school }}
        </h2>
        <div class="run-raffle">
          <button @click="runRaffle" >Run Raffle</button>
          <button @click="showWinners = true" >Show Winners</button>
        </div>
      </div>
    </div>
  </div>
  <div v-else class="main winners">
    <div class="content">
      <div class="raffle-main w-100" >
        <div class="grid">
          <div class="grid-item" v-for="(winner, key) in winners" :key="key">
          <h1>
            {{ winner.name }}
          </h1>
          <h2>
            {{ winner.school }}
          </h2>
          </div>
        </div>
        <div class="run-raffle">
          <button @click="resetWinners" >Hide Winners</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import _ from 'lodash';
import Papa from 'papaparse';

export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data() {
    return {
      winners: [],
      entries: [],
      winner: {
        name: '',
        school: ''
      },
      showWinners: false,
      hideEntries: false,
      entriesText: ''
    }
  },
  methods: {
    resetWinners() {
      this.winner = {
        name: '',
        school: ''
      };
      this.winners = [];
      this.showWinners = false;
    },
    delay(ms) {
      return new Promise(res => setTimeout(res, ms));
    },
    updateEntries() {
      this.entries = Papa.parse(this.entriesText).data;
    },
    async runRaffle() {
      this.entries = this.entries.filter(([name, school]) => {
        return !this.winners.find((winner) => winner.name === name && winner.school === school)
      })
      for (let i = 0; i < 100; i++) {
        const [ name, school ] = _.sample(this.entries);
        this.winner = {
          name,
          school
        };
        await this.delay(25)
      }

      this.winners.push({ ...this.winner });
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.main {
  width: 100vw;
  height: 100%;
  display: flex;
  flex-direction: column;
}
.header {
  display: flex;
  width: 100vw;
  position: absolute;
  top: 0
}
.content {
  width: 100vw;
  height: 100%;
  display: flex;
  flex-direction: row;
}
.grid {
  display: grid;
  justify-content: space-evenly;   
  width: 100%;
  grid-template-columns: repeat( auto-fit, minmax(400px, 1fr) );
}
.grid h1 {
  font-size: 40px;
  margin-top: 5px !important; 
  margin-bottom: 5px !important;
}
.grid h2 {
  font-size: 30px;
  margin-top: 5px !important; 
  margin-bottom: 30px !important;
}
textarea {
  width: 80%;
  height: 80%;
  resize: none;
}
.raffle-main {
  height: 100%;
}
.entries, .raffle-main {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}
.toggle-entries {
  background: none;
  border: none
}
.toggle-entries:hover {
  cursor: pointer;
}
.entries {
  width: 50%;
  height: 100%
}
.raffle-main {
  color: white;
  width: 50%;
  height: 100%;
  background-image: url(https://files.123freevectors.com/wp-content/uploads/new/123fv-images/1175-green-chalkboard-background.jpg);
  background-repeat: none;
  background-size: cover;
}
.w-100 {
  width: 100% !important
}
.d-none {
  display: none
}
h1, h2 {
  margin: 0;
  margin-bottom: 30px
}
.run-raffle {
  position: absolute;
  bottom: 10px
}
.run-raffle > button {
  cursor: pointer;
  font-size: 15px;
  color: white;
  padding: 5px 20px;
  border-radius: 10px;
  background: #736855;
  border: none;
  margin-left: 10px;
}
/* .run-raffle:hover {
  border: solid 1px #ad9d9d
} */
*:focus {
  outline: none
}
</style>
