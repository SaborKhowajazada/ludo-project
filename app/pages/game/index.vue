<template>
    <div>
        <h1>Number of players: {{ route.numberOfPlayers }}</h1>
        <div v-for="(player, index) in players" :key="player.label" :class="['player-aria', {'is-not-active': !player.isActive}]">    
            <p>player {{index + 1}}</p>    

            <ludo-dice :dice-disabled="!player.isActive || player.diceValue != 0" @click="handleClick(index)"/>
            <p>The player draw: {{player.diceValue}}</p>

            <game-token v-for="token in player.insideTokens" :key="token.label"  :token-disabled="player.diceValue != 6"  :label="'insideTokens'" :color="player.diceColor" @click="insideTokenHandle(index)"/>
            <game-token v-for="token in player.outSideTokens" :key="token.label"  :token-disabled="player.diceValue == 0"  :label="`token outside moved ${ token.position } steps`" :color="player.diceColor" @click="outSideTokenHandle(index, token.id)"/>

        </div>
    </div>
</template>


<script setup>
    const route = useRoute().query;

    // giving dice to user acording to number of players
    const players = ref([]);
    onMounted(() =>{
        const diceColors = ["green", "blue", "red", "yellow"];
        for(let i = 0; i < route.numberOfPlayers; i++){
            const playerData = { 
                label: i + 1, 
                isActive: true, 
                diceValue: 0,
                diceColor: diceColors[i],
                insideTokens: [
                  {label: 'token inside'},  
                  {label: 'token inside'},  
                  {label: 'token inside'},  
                  {label: 'token inside'},  
                ],
                outSideTokens: [] 
            };
            if(i > 0){
                playerData.isActive = false;
            }
            players.value.push(playerData);
        }
    })

    const handleClick = (index) =>{
        const randomDiceOutput = Math.floor(Math.random() * 6 + 1);
        // console.log(randomDiceOutput);
        players.value[index].diceValue = randomDiceOutput
        if(randomDiceOutput == 6 || players.value[index].outSideTokens.length != 0 ){
            return;
        }
        
        //The dice value is not showing up when the player draw a number
        players.value[index].diceValue = 0;
        players.value[index].isActive = false;
        if (index + 1 == route.numberOfPlayers) {
            players.value[0].isActive = true;
        } else {
            players.value[index +1].isActive = true;
        }
    }

    const insideTokenHandle = (index) =>{
        players.value[index].diceValue = 0;

        players.value[index].insideTokens.pop(); 

        players.value[index].outSideTokens.push({
            label: "outSideTokens",
            position: 0,
            id: Math.random()
        })
    }

    const outSideTokenHandle = (index, itemId) =>{
        const newPosition = players.value[index].diceValue + players.value[index].outSideTokens.find((item) =>item.id == itemId).position;
        players.value[index].outSideTokens.find((item) =>item.id == itemId).position = newPosition

        const tempDiceValue = players.value[index].diceValue;
        players.value[index].diceValue = 0;
        if(tempDiceValue == 6){
            return;
        }

        players.value[index].isActive = false;
        if (index + 1 == route.numberOfPlayers) {
            players.value[0].isActive = true;
        } else {
            players.value[index +1].isActive = true;
        }
    }
</script>

<style>
.player-aria {
    border: 1px solid red;
    margin-bottom: 24px;
}
.is-not-active{
    pointer-events: none;
    background-color: rgb(255, 141, 48);
}

</style>
