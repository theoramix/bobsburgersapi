<template>
    <div class="character-card">
        <img class="picture" :src="pictureUrl"/>
        <div>
            <h2 class="name">{{name}}</h2>
            <p class="gender">{{gender}}</p>
            <p class="occupation">{{occupation}}</p>
            <p class="firstEpisode">{{firstEpisode}}</p>
            <p class="voicedBy">{{voicedBy}}</p>
        </div>
    </div>
</template>

<script>
    export default{
        name:'CharacterCard',
        props:{
            name:String,
            gender:String,
            occupation:String,
            firstEpisode:String,
            voicedBy:String,
            pictureUrl:{type:String, default:"https://bobsburgers-api.…/images/characters/1.jpg"}
        }
    }
</script>

<style scoped>

.character-card{
    background-color: #BB0B0B   ;
    margin:5%;
    padding: 5%;
    width: 80%;
    border-radius: 10px;
    transition: transform 1s;
    transform-style: preserve-3d;
    position: relative;
}

img {
  transition: transform 0.3s;
  width: 30%;
  cursor: pointer;
}

img:hover {
  -ms-transform: scale(1.1);
  -webkit-transform: scale(1.1);
  transform: scale(1.1);
}

/* 
.infos {
  padding-left: 20px;
} */
</style>
