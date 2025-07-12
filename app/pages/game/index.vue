<template>
    <div>
        <h1>Number of players: {{ route.numberOfPlayers }}</h1>
        <button v-for="player in buttons" :key="player.label" :disabled="!player.isActive" @click="underClick">
            <p>Dice: {{ player.label }}</p>
        </button>
    </div>
</template>


<script setup>
    const route = useRoute().query;

    // giving to user dice based on their choice
    const buttons = ref([]);
    onMounted(() =>{
        for(let i = 0; i < route.numberOfPlayers; i++){
            const buttonData = {label: i +1, isActive: true};
            if(i > 0){
                buttonData.isActive = false;
            }
            buttons.value.push(buttonData);
        }
    })
    const underClick = () =>{
        const rndInt = Math.floor(Math.random() * 6 + 1);
        console.log(rndInt);

        // buttons.value[0] = {label: 1, isActive: false}
        // buttons.value[1] = {label: 2, isActive: true}

        let itemPosition = 0;
        for(let i = 0; i < route.numberOfPlayers; i++){
            if(buttons.value[i].isActive == true){
                buttons.value[i].isActive = false;
                itemPosition = i;
                break;
            }
        }
        if (itemPosition + 1 == route.numberOfPlayers) {
            buttons.value[0].isActive = true;
        } else {
            buttons.value[itemPosition +1].isActive = true;
        }
       

    }

</script>
