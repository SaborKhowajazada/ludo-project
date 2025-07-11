<template>
    <div class="highlight"><span class="text-design">Welcome</span> To <span class="text-design">The</span> Ludo <span class="text-design">Game</span></div>
    <h2 class="text-h-two">Play with friends</h2>
  <form @submit.prevent="startTheGame" id="player-form">
  <label><input type="radio" v-model="pick" name="players" value="2"> <span class="text-design">2 </span>player</label>
  <label><input type="radio" v-model="pick" name="players" value="3"> <span class="text-design">3 </span>player</label>
  <label><input type="radio" v-model="pick" name="players" value="4"> <span class="text-design">4 </span>player</label>

  <button type="submit" class="space-between">Start</button>
</form>
<h2>Don't know how to play?</h2> 
<p>Watch the video</p>
<iframe width="560" height="315" src="https://www.youtube.com/embed/xYXj9DwKHr4?si=uC-Ymor9jx98sc8_" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
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
        margin-top: 120px;
        margin-bottom: 150px;
        font-weight: 700;
        font-size: 50px;
        
    }
    #player-form, .text-h-two, .space-between {
        text-align: center;
        width: 100%;
        font-size: 30px;
        margin-bottom: 40px;
    }
    form {
        display: flex;
        flex-direction: column;
        gap: 12px;
        font-size: 25px;
    }
    .text-design{
        color: rgba(255, 0, 0, 0.883);
    }
</style>