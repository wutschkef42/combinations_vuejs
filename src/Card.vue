<template>
    
    <div v-if="is_clicked == 1" class="card grid-item clicked">
        <p>{{ this.word }}</p>
    </div>
    <div v-else-if="is_clicked == 2" class="card grid-item winner">
        <p>{{ this.word }}</p>
    </div>
    <div v-else-if="is_clicked == 3" class="card grid-item loser">
        <p>{{ this.word }}</p>
    </div>
    
    <div v-else-if="is_highlight == 1" class="card grid-item highlight">
        <p>{{ this.word }}</p>
    </div>
    <div v-else class="card grid-item blank">
        <p>{{ this.word }}</p>
    </div>
</template>

<script>
export default {
  name: 'card',
  data () {
    return {
      
    }
  },
  props: ['word', 'is_clicked', 'is_highlight'],
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin: 0 auto;
  margin-top: 60px;
  width: 900px;
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


.grid-item {
  
  border: 1px solid rgba(0, 0, 0, 0.8);
  padding: 20px;
  align-self: center;
  font-size: 30px;
  text-align: center;
  cursor: pointer;
  height: 120px;
}

.clicked {
    background-color: rgba(255, 255, 255, 0.4);
}

.highlight {
    background-color: rgba(255, 255, 255, 0.6);
}

.blank {
    background-color: rgba(255, 255, 255, 0.8);
}

.winner {
    background-color: green;
}

.loser {
    background-color: red;
}



.grid-item p {
    position: relative;
    vertical-align: middle;
    
}

</style>
