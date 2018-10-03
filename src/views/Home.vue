<template>
  <div class="home">
    <h1>Welcome</h1>
    <p>
      For guide and recipes on how to configure / customize this project,<br>
      check out the
      <a href="https://cli.vuejs.org" target="_blank" rel="noopener">vue-cli documentation</a>.
    </p>
    <button @click="getNextCharacter">NEXT</button>
    <button @click="getPrevCharacter">Previous</button>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'home',
  data (){
    return {
      characterNumber: null,
      character: null,
      errors: []
    }
  },
  mounted () {
    this.randomNumber()
  },
  methods: {
    randomNumber () {
      this.characterNumber = Math.floor(Math.random() * 87) + 1;
      console.log(this.characterNumber);
      this.getCharacter();
    },
    async getCharacter () {
      let url = 'https://swapi.co/api/people/'+this.characterNumber.toString();
      console.log(url);
      const response = await axios.get(url);
      this.character = response.data;
      console.log(this.character.name);
      /*axios.get(url)
        .then(response => {
          console.log(response.data)
          this.character = response.data;
        })
        .catch(e => {
          this.errors.push(e)
        });*/
      //console.log(this.character);
    },
    getNextCharacter () {
      this.characterNumber++;
      console.log(this.characterNumber);
      this.getCharacter();
    },
    getPrevCharacter () {
      this.characterNumber--;
      console.log(this.characterNumber);
      this.getCharacter();
    }
  }
}
</script>
