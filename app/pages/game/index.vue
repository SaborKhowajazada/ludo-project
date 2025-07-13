<template>
    <div>
        <h1>Number of players: {{ route.numberOfPlayers }}</h1>
        <div v-for="(player, index) in players" :key="player.label">        
            <button :disabled="!player.isActive || player.diceValue == 6" @click="handleClick(index)">
                <p>Dice: {{ player.label }}</p>
            </button>
            <p>player draw: {{player.diceValue}}</p>
            <select v-if="player.diceValue == 6" @change="playersChoice(index)">
                <option>Draw token</option>
                <option>Move token</option>
            </select>
            <hr>
            <br>
            <br>
        </div>
    </div>
</template>


<script setup>
    const route = useRoute().query;

    // giving dice to user acording to number of players
    const players = ref([]);
    onMounted(() =>{
        for(let i = 0; i < route.numberOfPlayers; i++){
            const playerData = {label: i + 1, isActive: true, diceValue: 0 };
            if(i > 0){
                playerData.isActive = false;
            }
            players.value.push(playerData);
        }
    })

    const handleClick = (index) =>{
        const randomDiceOutput = Math.floor(Math.random() * 6 + 1);
        console.log(randomDiceOutput)
        players.value[index].diceValue = randomDiceOutput
        if(randomDiceOutput == 6){
            return;
        }
        
        players.value[index].isActive = false;
        if (index + 1 == route.numberOfPlayers) {
            players.value[0].isActive = true;
        } else {
            players.value[index +1].isActive = true;
        }
    }

    const playersChoice =(index) =>{
        players.value[index].diceValue = 0;
    }

</script>

