<template>
    <button :disabled="diceDisabled" @click="onClick">
        Label
    </button>
</template>


<script setup>
    defineProps(['diceDisabled']);

    const emits = defineEmits(['click']);
    const onClick = ()=>{
        emits('click')
    }

</script>