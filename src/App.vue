<template>
  <div id="app">
    <router-view/>
  </div>
</template>

<script>
export default {
  name: 'App'
}
</script>

<style>
#app,body,
html {
 
    height: 100%;
    overflow: auto;
    position: relative;

}
*{
   margin: 0;
  padding: 0;
}
</style>
