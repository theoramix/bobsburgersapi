<template>
  <div id="app">
    <Header/>
           <div class="gallery-options">
            <input type="text" v-model="search" placeholder="Chercher un personnage"/>
            <button v-if="search" @click="cleanSearch">X</button>
            <label for="character-sort">Trier par : </label>
				<select v-model="charactersSortType" id="character-sort">
				  <option value="AZName">Noms de A à Z</option>
				  <option value="ZAName">Noms de Z à A</option>
				</select>
        </div>
    <CharactersGallery :charactersData="charactersOrganizeData"/>
    <Footer />
  </div>
</template>

<script>
import CharactersGallery from './components/CharactersGallery.vue'
import axios from 'axios'
import Header from './components/Header.vue'
import Footer from "./components/Footer.vue";

export default {
  name: 'App',
  components: {
    CharactersGallery,
    Header,
    Footer,
  },

	watch: {
		search: function(newSearch) {
			localStorage.setItem("search", newSearch)
		},
		charactersSortType: function(newcharactersSortType) {
			localStorage.setItem("charactersSortType", newcharactersSortType)
		}
	},

	created: function() {
		this.retrievecharactersData()
	},

	computed: {
		charactersOrganizeData: function() {
			const field = ["AZName", "ZAName"].includes(this.charactersSortType) ? "name" : "breed"
			const reversed = ["ZAName", "ZABreed"].includes(this.charactersSortType)
      console.log(field)
      console.log(reversed)
			const filterFunc = (a) => a.name.toLowerCase().includes(this.search.toLowerCase())
			const comparator = (a, b) => a[field].localeCompare(b[field]) 
			let data = this.charactersData.filter(filterFunc)
			data = data.sort(comparator)
			if (reversed) data = data.reverse()
			return data
		}
	},
  
  methods: {
		cleanSearch: function() {
		this.search = ""}	
	},

  data() {
    return {
      charactersData: [],
			search: localStorage.getItem("search") || "",
			charactersSortType: localStorage.getItem("charactersSortType") || "AZName"
    }
  },

  mounted() {
    // Make a request for a user with a given ID
axios.get('https://bobsburgers-api.herokuapp.com/characters/')
  .then((response)=> {
    // handle success
    this.charactersData=response.data;
    console.log(response);
  })
  .catch(function (error) {
    // handle error
    console.log(error);
  })

  } 
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: black;
  background: #C7B7BA;
}
</style>
<!-- -->