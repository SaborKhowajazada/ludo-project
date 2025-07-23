<template>
    <main class="board"> 
        <div 
            v-for="(player, index) in players" 
            :key="player.label" 
            :class="['player-area', { 'is-not-top': index == 2 || index == 3}, `player-${player.label}`]"
        >    
            <ludo-path class="path" :player-number="player.label"/>
            <div class="initial-cell">
            <ludo-dice 
                :is-active="player.isActive" 
                :color="player.tokenColor" 
                :dice-value="player.diceValue" 
                :dice-disabled="!player.diceCanBeClicked" 
                @click="handleClick(index)"
            />
            <div class="player-tokens">
                <game-token  v-for="token in player.insideTokens" :key="token.label" :token-disabled="player.diceValue != 6" :label="'insideTokens'" :color="player.tokenColor" @click="insideTokenHandle(index)"/>
            </div>
            <game-token v-for="token in player.outSideTokens" :key="token.label"  :token-disabled="player.diceValue == 0"  :label="`token outside moved ${ token.position } steps`" :color="player.tokenColor" @click="outSideTokenHandle(index, token.id)"/>
            </div>
        </div>
    </main>
</template>



<script setup>
    const props = defineProps(['numberOfPlayers']);

    // giving dice to user acording to number of players
    const players = ref([]);
    onMounted(() =>{
        const tokenColors = ["green", "blue", "red", "yellow"];
        for(let i = 0; i < props.numberOfPlayers; i++){
            const playerData = { 
                label: i + 1, 
                isActive: true, 
                diceValue: 0,
                diceCanBeClicked: true,
                tokenColor: tokenColors[i],
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
        //console.log(randomDiceOutput);
        players.value[index].diceValue = randomDiceOutput
        players.value[index].diceCanBeClicked = false;
        if(randomDiceOutput == 6 || players.value[index].outSideTokens.length != 0 ){
            return;
        }
        
        //The dice value is not showing up when the player draw a number
        players.value[index].diceCanBeClicked = true;
        //players.value[index].diceValue = 0;
        players.value[index].isActive = false;

        if (index + 1 == props.numberOfPlayers) {
            players.value[0].isActive = true;
        } else {
            players.value[index +1].isActive = true;
        }
    }

    const insideTokenHandle = (index) =>{
        players.value[index].diceValue = 0;
        players.value[index].diceCanBeClicked = true;

        players.value[index].insideTokens.pop(); 

        players.value[index].outSideTokens.push({
            label: "outSideTokens",
            position: 0,
            id: Math.random()
        })
    }

    const outSideTokenHandle = (index, itemId) =>{
        players.value[index].diceCanBeClicked = true;
        const newPosition = players.value[index].diceValue + players.value[index].outSideTokens.find((item) =>item.id == itemId).position;
        players.value[index].outSideTokens.find((item) =>item.id == itemId).position = newPosition

        const tempDiceValue = players.value[index].diceValue;
        players.value[index].diceValue = 0;
        if(tempDiceValue == 6){
            return;
        }

        players.value[index].isActive = false;
        if (index + 1 == props.numberOfPlayers) {
            players.value[0].isActive = true;
        } else {
            players.value[index +1].isActive = true;
        }
    }
</script>


<style scoped>
/* .initial-cell {
    border: 3px solid green;
} */
.player-area {
    display: flex;
    flex-direction: column;
    justify-content: space-evenly;
}

.player-1 {
    flex-direction: column-reverse;
    border: 3px solid green;
}

.player-2 {
    flex-direction: row;
    border: 3px solid blue;
}

.player-3 {
    flex-direction: row-reverse;
    border: 3px solid red
}

.player-4 {
    flex-direction: column;
    border: 3px solid yellow;
}
/* .player-area.is-not-top {
    flex-direction: column-reverse;
} */

.player-tokens {
    margin-bottom: 0px;
}
.is-not-active{
    pointer-events: none;
    cursor: not-allowed;
}

.board{
    border: 1px solid red;
    min-height: 70vh;
    max-width: 70vw;
    margin: 0px 0px;
    display: grid;
    grid-template-areas: 
        "pOne pTwo" 
        "pThree pFour";
    grid-template-columns: 1fr 1fr;
    grid-template-rows: 1fr 1fr;
    grid-gap: 24px;
}

.player-area:first-child {
    grid-area: pOne;
}

.player-area:nth-child(2){
    grid-area: pTwo;
}

.player-area:nth-child(3){
    grid-area: pThree;
}
.player-area:last-child{
    grid-area: pFour;
}

</style>
