<template>
    <div class="task" :id="task.id">
        <span :class="task.id">{{task.id}}</span><span :class="task.status">{{task.name}}</span>
    </div>
</template>
<script>
export default {
    name:"Task",
    props:
    {
        task: {type: Object, required:true},  
    },
    
}
</script>