<template>
    <div>
        <h1>Number of players: {{ route.numberOfPlayers }}</h1>
        <button v-for="player in numberOfButtons" :key="player">
            <p>Dice: {{ player }}</p>
        </button>
    </div>
</template>




<script setup>
    const route = useRoute().query;

const numberOfButtons = computed(() => {
    const buttons = []
    for (let i = 0; i < route.numberOfPlayers; i++) {
        buttons.push(i + 1)
    }
    return buttons;
})
</script>