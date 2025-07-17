<template>
    <button :class="[color, 'buttonColor']" :disabled="tokenDisabled"  @click="onClick">
        {{ label }}
    </button>
</template>




<script setup>
defineProps(["label", "color", "tokenDisabled"]);
const emits = defineEmits(["click"]);

const onClick = ()=>{
    emits('click')
}

</script>

<style>

.green{
    background-color: green;
}
.blue{
    background-color: blue;
}
.red{
    background-color: red;
}
.yellow{
    background-color: yellow;
}

.buttonColor{
    color: white;
    margin-bottom: 10px;
    margin-left: 5px;
    font-size: 18px;
    padding: 8px;
    text-align: center;
    cursor: pointer;
    border-radius: 12px;
    box-shadow: 0 4px black;
}

.buttonColor:hover{
    background-color: gray;
}


</style>