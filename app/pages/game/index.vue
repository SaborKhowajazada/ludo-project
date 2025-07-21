<template>
    <ludo-board :number-of-players="route.numberOfPlayers"/>
</template>


<script setup>
    const route = useRoute().query;
</script>

