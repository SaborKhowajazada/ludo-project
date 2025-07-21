<template>
    <main class="board"> 
        <slot/>
    </main>
</template>




<style>
.board{
    border: 1px solid red;
    min-height: 70vh;
    max-width: 70vh;
    margin: 0px 0px;
    display: grid;
    grid-template-areas: "p1 squares p2" "squares squares squares" "p3 squares p4";
    grid-template-columns: 1fr 1fr 1fr;
    grid-template-rows: 1fr 1fr 1fr;
}

.board:first-child {
    grid-area: p1;
}

.board:nth-child(2){
    grid-area: p2;
}

.board:nth-child(3){
    grid-area: p3;
}
.board:last-child{
    grid-area: p4;
}

</style>
