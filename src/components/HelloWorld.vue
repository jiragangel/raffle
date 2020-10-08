<template>
  <div class="main">
    <div class="header">
      <button @click="hideEntries = false">Show Entries</button>
      <button @click="hideEntries = true">Hide Entries</button>
    </div>
    <div class="content">
      <div class="entries" :class="{
        'd-none': hideEntries
      }">
        <textarea @input="updateEntries" />
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
        <button @click="runRaffle">Run Raffle</button>
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
      entries: [],
      winner: {
        name: '',
        school: ''
      },
      hideEntries: false
    }
  },
  methods: {
    delay(ms) {
      return new Promise(res => setTimeout(res, ms));
    },
    updateEntries(event) {
      const {
        target: {
          value
        }
      } = event;
      this.entries = Papa.parse(value).data;
    },
    async runRaffle() {
      for (let i = 0; i < 100; i++) {
        const [ name, school ] = _.sample(this.entries);
        this.winner = {
          name,
          school
        };
        await this.delay(25)
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.main {
  width: 100vw;
  height: 100vh;
  display: flex;
  flex-direction: column;
}
.content {
  width: 100vw;
  height: 100%;
  display: flex;
  flex-direction: row;
}
textarea {
  width: 80%;
  height: 80%;
  resize: none;
}
.entries, .raffle-main {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}
.entries {
  width: 50%;
  height: 100%
}
.raffle-main {
  width: 50%;
  height: 100%
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
</style>
