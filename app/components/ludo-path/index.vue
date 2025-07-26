<template>
  <div :class="['path-container', `player-path-${playerNumber}`]">

    <div class="path path1">
      <div v-for="cell in cells" :key="cell" :class="['cell', `cell-${ cell }`]" >
        {{ cell }}
      </div>
    </div>

    <div class="path path2">
      <div v-for="cell in cells" :key="cell" :class="['cell', `cell-${ cell }`]">
        {{ cell }}
      </div>
      <!-- <div class="cell">
        7
      </div> -->
    </div>

    <div class="path path3">
      <div v-for="cell in cells" :key="cell" :class="['cell', `cell-${ cell }`]">
        {{ cell }}
      </div>
    </div>

  </div>
</template>

<script setup>
const cells = ref([1, 2, 3, 4, 5, 6]);
defineProps(['playerNumber'])
</script>

<style scoped>


.player-path-1 .path1 .cell-2,
.player-path-1 .path2 .cell-2,
.player-path-1 .path2 .cell-3, 
.player-path-1 .path2 .cell-4, 
.player-path-1 .path2 .cell-5, 
.player-path-1 .path2 .cell-6,
.player-path-1 .path3 .cell-3
 {
  background-color: green;
}

.player-path-2 .path3 .cell-2,
.player-path-2 .path2 .cell-2,
.player-path-2 .path2 .cell-3,
.player-path-2 .path2 .cell-4,
.player-path-2 .path2 .cell-5,
.player-path-2 .path2 .cell-6,
.player-path-2 .path1 .cell-3
{
  background-color: blue;
}

.player-path-3 .path1 .cell-2,
.player-path-3 .path2 .cell-2,
.player-path-3 .path2 .cell-3,
.player-path-3 .path2 .cell-4,
.player-path-3 .path2 .cell-5,
.player-path-3 .path2 .cell-6,
.player-path-3 .path3 .cell-3
{
  background-color: red;
}

.player-path-4 .path3 .cell-2,
.player-path-4 .path2 .cell-2,
.player-path-4 .path2 .cell-3,
.player-path-4 .path2 .cell-4,
.player-path-4 .path2 .cell-5,
.player-path-4 .path2 .cell-6,
.player-path-4 .path1 .cell-3
{
  background-color: yellow;
}

.path-container {
  display: flex;
}


.player-path-1 .path {
  display: flex;
} 

.player-path-4 {
  flex-direction: column;
}

.player-path-4 .path {
  display: flex;
  flex-direction: row-reverse;
} 

.player-path-3 .path {
  display: flex;
  flex-direction: column-reverse;
} 


.player-path-1 {
  flex-direction: column;
  grid-area: 2 / 2 / 3 / 4;
  
}


.player-path-2{
  grid-area: 1/1/3/2;
}

.player-path-2 .path{
  display: flex;
  flex-direction: column;
}

.player-path-3{
  grid-area: 1 / 3 / 3 / 4;
}


.player-path-4{
  grid-area: 1 / 1 / 2 / 3;
}

.path {
  width: 100%;
  height: 100%;
}


.cell {
  width: 100%;
  height: 100%;
  border: 3px solid black;
}
</style>
