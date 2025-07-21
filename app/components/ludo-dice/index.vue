<template>
    <button class="button-style" :disabled="diceDisabled" @click="onClick" >
        <LudoDiceDiceFaceOne v-if="diceValue == 0 || diceValue == 1"/>
        <LudoDiceDiceFaceTwo v-else-if="diceValue == 2"/>
        <LudoDiceDiceFaceThree v-else-if="diceValue == 3"/>
        <LudoDiceDiceFaceFour v-else-if="diceValue == 4"/>
        <LudoDiceDiceFaceFive v-else-if="diceValue == 5"/>
        <LudoDiceDiceFaceSex v-else-if="diceValue == 6" />
        <GameToken :color="color"/>
    </button>
</template>


<script setup>
    defineProps(['diceDisabled', 'diceValue', 'color']);

    const emits = defineEmits(['click']);
    const onClick = ()=>{
        emits('click')
        
    }
</script>

<style scoped>
    .button-style{
        border: none;
        padding: 0px;
        
    }
</style>


