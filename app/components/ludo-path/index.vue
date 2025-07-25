<template>
  <div :class="['path-container', `player-path-${playerNumber}`]">

    <div class="path path1">
      <div v-for="cell in cells" :key="cell" class="cell">
        {{ cell }}
      </div>
    </div>

    <div class="path path2">
      <div v-for="cell in cells" :key="cell" class="cell">
        {{ cell }}
      </div>
      <div class="cell">
        7
      </div>
    </div>

    <div class="path path3">
      <div v-for="cell in cells" :key="cell" class="cell">
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
.path-container {
  display: flex;
}


.player-path-1 .path {
  display: flex;
  width: 400px;
} 

.player-path-4 {
  flex-direction: column;
}

.player-path-4 .path {
  display: flex;
  flex-direction: row-reverse;
  width: 400px;
} 

.player-path-3 .path {
  display: flex;
  flex-direction: column-reverse;
} 


.player-path-1 {
  flex-direction: column;
  grid-area: 2 / 1 / 3 / 3;
}


.player-path-2{
  grid-area: 1/1/3/2;

}

.player-path-3{
  grid-area: 3 / 2 / 1 / 3;
}

.player-path-4{
  grid-area: 1 / 1 / 2 / 3;
}

.path {
  width: 48px;
}


.cell {
  width: 48px;
  height: 48px;
  border: 2px solid greenyellow;
}
</style>
