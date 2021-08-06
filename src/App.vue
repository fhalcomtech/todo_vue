<template>
  <Todo/>
</template>

<style lang="scss">

$azure: hsla(211, 100%, 50%, 1);
$slate-gray: hsla(208, 7%, 46%, 1);
$green-pantone: hsla(134, 61%, 41%, 1);
$rusty-red: hsla(354, 70%, 54%, 1);
$mikado-yellow: hsla(45, 100%, 52%, 1);
$pacific-blue: hsla(188, 76%, 41%, 1);
$gunmetal: hsla(210, 10%, 23%, 1);
$cultured: hsla(210, 17%, 98%, 1);

*, *:before, *:after{
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  }

   #app
   {
    background-color: $gunmetal;
    color:$cultured;
    height: 100vh;
  }
</style>

<script>

import Todo from "@/views/Todo";

export default {
  name: "App",
  components:{
    Todo,
  }
}
</script>
