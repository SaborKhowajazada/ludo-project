<template>
    <main class="board"> 
        <div 
            v-for="(player, index) in players" 
            :key="player.label" 
            :class="['player-area', { 'is-not-top': index == 2 || index == 3}, `player-${player.label}`]"
        >    
            <ludo-path :player-number="player.label"/>
            <div class="initial-cell">
            <!-- <ludo-dice 
                :is-active="player.isActive" 
                :color="player.tokenColor" 
                :dice-value="player.diceValue" 
                :dice-disabled="!player.diceCanBeClicked" 
                @click="handleClick(index)"
            /> -->
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
.initial-cell {
    border: 70px solid green;
}
.player-area {
    display: flex;
    flex-direction: column;
    justify-content: space-evenly;
}

.player-1 {
    flex-direction: column-reverse;
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    grid-template-rows: 2fr 1fr;
}
.player-1 .initial-cell{
    grid-area: 1/1/2/3;
}


.player-2 {
    flex-direction: row;
    display: grid;
    grid-template-columns: 1fr 2fr;
    grid-template-rows: repeat(2, 1fr);
}
.player-2 .initial-cell{
    grid-area: 1/2/3/3;
    border-color: blue;
}

.player-3 {
    flex-direction: row-reverse;
    display: grid;
    grid-template-columns: 2fr 1fr;
    grid-template-rows: repeat(2, 1fr);
}

.player-3 .initial-cell{
    grid-area: 1 / 1 / 3 / 2;
    border-color: red;
}


.player-4 {
    flex-direction: column;
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    grid-template-rows: 1fr 2fr;
}

.player-4 .initial-cell{
    grid-area: 2/ 1 / 3 / 3;
    border-color: yellow;
}

/* .player-area.is-not-top {
    flex-direction: column-reverse;
} */

.player-tokens {
    border: 3px solid black;
    margin-bottom: 0px;
    width: 100%;
    height: 100%;
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-template-rows: 1fr 1fr;
    
}

.is-not-active{
    pointer-events: none;
    cursor: not-allowed;
}

.board{
    border: 3px solid black;
    min-height: 90vh;
    max-width: 90vh;
    margin-inline: auto;
    display: grid;
    grid-template-areas: 
        "pOne pTwo pTwo" 
        "pOne square pFour "
        "pThree pThree pFour";
    grid-template-columns: 2fr 1fr 2fr;
    grid-template-rows: 2fr 1fr 2fr;
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
