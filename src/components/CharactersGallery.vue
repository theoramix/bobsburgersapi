<template>
   <div class="galery">
        <div class="characters-gallery">
        <CharacterCard
        v-for="character in charactersData"
        :key="character.id"
        :name="character.name"
        :gender="character.gender"
        :occupation="character.occupation"
        :firstEpisode="character.firstEpisode"
        :voicedBy="character.voicedBy"
        :pictureUrl="character.image"/>
        </div>
   </div>
</template>

<script>
import CharacterCard from './CharacterCard.vue'
export default{
    name:'CharactersGallery',
    data() {
        return {
            charactersData: [],
			search: "",
			charactersSortType: "AZName"
            }
    },

    props: {
        charactersData: {
        },
    },
    
    components: {
        CharacterCard
    },
}
</script>

<style>
.characters-gallery {
    display: grid;
    grid-template-columns: 25% 25% 25%;
    justify-content: center;
    border: 5px;
}
</style>