<template>
  <div class="home">
    <h1>Star Wars Character Info</h1>
    <h2>{{character.name}}</h2>
    <h3>Birth year: {{character.birth_year}}</h3>
    <button v-show="characterNumber > 1" @click="getPrevCharacter">Previous</button>
    <button v-show="characterNumber < 87" @click="getNextCharacter">NEXT</button>
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
      homeplanet: null,
      starship: [],
      shipInfo: [],
      planetInfo: [],
      errors: []
    }
  },
  mounted () {
    this.randomNumber()
  },
  components: {
    'homeworlds':{
      template: ''
    },
    'spaceship':{
      template: ''
    }
  },
  methods: {
    randomNumber () {
      this.characterNumber = Math.floor(Math.random() * 87) + 1;
      console.log(this.characterNumber);
      this.getCharacterInfo();
    },
    async getCharacterInfo () {
      //clear the starship array
      this.starship = [];

      //call API for character info with random generated character id number
      let url = 'https://swapi.co/api/people/'+this.characterNumber.toString();
      console.log(url);
      const response = await axios.get(url);
      this.character = response.data;

      //put the homeplanet info into its variable
      this.homeplanet = this.character.homeworld;

      //check if the homeplanet variable is still null if not call the getPlanet method
      if(this.homeplanet !== null){
        this.getPlanet();
      }

      //check to see is character is tied to any starships and push info into the starship array
      if(this.character.starships.length > 0){
        this.character.starships.forEach((starship) => {
          this.starship.push(starship);
        });
      }

      //check to see anything was added to the starship array
      if(this.starship.length > 0){
        //if so do an API call for the starships and push into the shipInfo array
        this.getShip();
        }

      console.log(this.character);
    },
    getShip () {
      this.shipInfo = [];
      this.starship.forEach((ship) => {
        axios.get(ship)
          .then(response => {
            this.shipInfo.push(response.data);
            console.log(this.shipInfo);
          })
      })
    },
    getPlanet () {
      this.planetInfo = [];
      axios.get(this.homeplanet)
        .then(response => {
          this.planetInfo.push(response.data);
          console.log(this.planetInfo[0]);
        })
    },
    getNextCharacter () {
      this.characterNumber++;
      console.log(this.characterNumber);
      this.getCharacterInfo();
    },
    getPrevCharacter () {
      this.characterNumber--;
      console.log(this.characterNumber);
      this.getCharacterInfo();
    }
  }
}
</script>
