<template>
   <Tasks :task="task"/>
</template>
<style lang="scss" scoped>

</style>

<script>
import Tasks from "@/components/Tasks"
export default 
{
   name: "Todo",
   components:{
       Tasks
   },
   props:
   {
       tasks_list:{
           type:Array,
           defaul:this.fnGetTask()
       },
       corrent_task:{
           type:Object
       }
   },
   methods:
   {
       fnGetTask: async () => await  fetch("http://localhost:7777/todo")
       .then(result => result.json())
       .then(data_json=>data_json)
       .catch((err) => {console.error(err)})
   }



};
</script>
