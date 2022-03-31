<script setup>
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup
import HelloWorld from './components/HelloWorld.vue'
import BindModel from './components/BindModel.vue'
import ClickCounter from './components/ClickCounter.vue';
import VIF from './components/VIF.vue';
import VFor from './components/VFor.vue';
import Computed from './components/Computed.vue';
import VIFR from './components/VIFR.vue';
import Date from './components/Date.vue';
</script>

<template>
  <img alt="Vue logo" src="./assets/logo.png" />
  <!-- <HelloWorld msg="Hello Vue 3 + Vite" /> -->
  <!-- <BindModel/> -->
  <!-- <ClickCounter/> -->
  <!-- <VIF/> -->
  <!-- <VFor/> -->
  <!-- <Computed/> -->
  <!-- <VIFR/> -->
  <Date/>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
