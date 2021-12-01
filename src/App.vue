<template>
  <div id="app">
<!--    <TheMain/>-->
    <the-content/>
    <TheSidebar/>
    <the-footer/>
  </div>
</template>

<script>
import TheContent from "@/components/TheContent";
import TheFooter from "@/components/TheFooter";
import TheMain from "@/components/TheMain";
import TheSidebar from "@/components/TheSidebar";

export default {
  name: 'App',
  components: {TheSidebar, TheMain, TheContent, TheFooter}
};
</script>

<style>
#app {
  color: #3C374A;
  background-image: linear-gradient(transparent 98%, #BDBDBD 98%),
  linear-gradient(to right, transparent 98%, #BDBDBD 98%);
  background-size: 30px 30px;
  background-repeat: repeat;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  height: 100vh;
  overflow: hidden;
}
</style>
