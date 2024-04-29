<template>
  <Header />
  <div>
    <router-view />
  </div>
  <Footer />
</template>

<script setup>
import Footer from "./components/Footer.vue";
import Header from "./components/Header.vue";
</script>

<style>
body {
  min-height: 100vh;
  width: 100%;
  background-color: #141414;
  color: #f7f8f8;
  overflow-x: hidden;
}
</style>
