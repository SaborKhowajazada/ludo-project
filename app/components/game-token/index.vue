<template>
    <button :class="[color, 'buttonColor']" :disabled="tokenDisabled"  @click="onClick">
        <svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" width="42px" height="60px" viewBox="0 0 42 59" version="1.1">
        <g id="surface1">
        <path style="fill-rule:nonzero;fill-opacity:1;stroke-width:3.4132;stroke-linecap:butt;stroke-linejoin:miter;stroke:rgb(0%,0%,0%);stroke-opacity:1;stroke-miterlimit:4;" d="M 304.691287 1.672246 C 193.588788 1.672246 103.599225 87.026459 103.599225 192.377944 C 103.599225 270.555435 153.23193 337.723975 224.254462 367.12763 L 154.754831 540.065717 L 1.703351 921.128729 L 3.157029 921.128729 C 2.326356 923.497744 1.980242 925.866759 1.980242 928.235774 C 1.980242 972.48061 137.3107 1008.224864 304.414396 1008.224864 C 471.518092 1008.224864 607.056218 972.48061 607.056218 928.235774 C 607.056218 927.608681 606.986995 926.981589 606.917772 926.354497 L 607.748445 926.354497 L 605.948654 921.825498 C 605.60254 920.640991 605.187204 919.456483 604.633422 918.271976 L 457.673544 542.713439 L 388.520026 365.664415 C 457.742766 335.494314 505.852571 269.231574 505.852571 192.308267 C 505.852571 87.026459 415.724563 1.672246 304.691287 1.672246 Z M 304.691287 1.672246 " transform="matrix(0.0564302,0,0,0.0560623,0.00544213,0)"/>
        </g>
        </svg>
        
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

.green path{
    fill: green;
}
.blue path{ 
    fill: blue;
}
.red path{
   fill: red;
}
.yellow path{
    fill: yellow;
}

.buttonColor{
    border: none;
    padding: 0%;
    background-color: transparent;
}


</style>