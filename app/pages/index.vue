<template>
    <div class="highlight">Welcome to the Ludo game!</div>
    <h2 class="text-h-two">How many players are there?</h2>
  <form @submit.prevent="startTheGame" id="player-form">
  <label><input type="radio" v-model="pick" name="players" value="2"> 2 player</label>
  <label><input type="radio" v-model="pick" name="players" value="3"> 3 player</label>
  <label><input type="radio" v-model="pick" name="players" value="4"> 4 player</label>

  <button type="submit" class="space-between">Start the game</button>
</form>

</template>

<script setup>
const pick = ref("2")
function startTheGame(){
console.log("The game starts with ", pick.value, "people")
}
</script>


<style>
    .highlight {
        text-align: center;
        height: 70px;
        margin-top: 60px;
        color: rgba(255, 0, 0, 0.883);
        font-weight: 700;
    }
    #player-form, .text-h-two {
        text-align: center;
        width: 100%;
    }
    form {
        display: flex;
        flex-direction: column;
        gap: 12px;
    }
</style>