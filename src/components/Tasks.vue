<template>
    <div v-if="fnGetNumberTask">
        <h3>Listo</h3>
    </div>
    <div v-else> 
        <h3>No existen datos</h3>
    </div>
</template>


<script>
export default {

    name: "Task",
    props:{
        tasks:Array
        },
    computed:{
        fnGetNumberTask:  () => {return (this.tasks>0)}
}
}
</script>