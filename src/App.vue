<template>
  <div id="app">
    <h1>Find The Right Combination</h1>
    <p> Select {{ this.word_count }} other words.</p>
    <div class="grid-container">
      <a v-for="(word, index) in word_list" :key=index
        v-on:click="handleClick(index)"
        v-on:mouseover="highlightCard(index)">
        <card :word=word.str v-bind:is_clicked=word.is_clicked v-bind:is_highlight=word.is_highlight />
      </a>
      
    </div>
  </div>
</template>

<script>
import Card from './Card'

let initGameState = (word_list) => {
  console.log("init")
  return (word_list.map((w,index) => ({ str: w.str, is_clicked: 0, is_winner: w.is_winner, is_highlight: 0 })))
}

let cardToString = (card) => {
  console.log(card.str + " - " + card.is_clicked + " - " + card.is_winner);
}

export default {
  name: 'app',
  components: { Card },
  data () {
  
    const word_list = [
      { str: 'Résistante', is_winner: 1 },
      { str: 'Matériaux froid', is_winner: 0 },
      { str: 'Inoxydable', is_winner: 1 },
      { str: 'Indice de réfraction éléve', is_winner: 1 },
      { str: 'Oxydable', is_winner: 0 },
      { str: 'Fragile', is_winner: 0 },
      { str: 'Confortable', is_winner: 1 },
      { str: 'Matériaux chaud', is_winner: 1 },
      { str: 'Indice de réfraction faible', is_winner: 0 },
    ];

    return {
      game_over: 0,
      word_count: 5,
      click_state: 0,
      current_highlight: -1,
      word_list: initGameState(word_list),
    }
  },
  methods: {

    handleClick: function(index) {
      
      this.word_list[index].is_clicked = this.word_list[index].is_clicked ? 0 : 1;
      this.word_count = this.word_list[index].is_clicked ?
        this.word_count - 1 : this.word_count + 1;
      if (this.game_over) {
        this.word_list = initGameState(this.word_list);
        this.word_count = 5;
        this.game_over = 0;
      }
      if (this.word_count == 0) {
        if (this.checkWinner()) {
          this.word_list = this.word_list.map(w =>
            ({ str: w.str, is_clicked: w.is_clicked ? 2 : 0, is_winner: w.is_winner, is_highlight: 0 })) 
        } else {
          this.word_list = this.word_list.map(w => (
            { str: w.str, is_clicked: w.is_clicked ? 3 : 0, is_winner: w.is_winner, is_highlight: 0 }))
        }
        this.game_over = 1;
      }
    },
    highlightCard(index) {  
      if (this.current_highlight >= 0) {
        this.word_list[this.current_highlight].is_highlight = 0;
      }
      this.current_highlight = index;
      this.word_list[index].is_highlight = 1;
    },
    checkWinner: function() {
      this.word_list.map(s => cardToString(s));
      return (this.word_list.reduce((acc, cur) => ( acc && (!cur.is_clicked || cur.is_winner )), true));
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}



.grid-container {
  display: grid;
  grid-template-columns: auto auto auto;
  background-color: #2196F3;

}
</style>
