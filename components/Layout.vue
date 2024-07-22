<template>
    <a-layout>
      <Header />
      <a-layout-content class="content">
        <slot />
      </a-layout-content>
      <Footer />
    </a-layout>
  </template>
  
  <script setup>
  import Header from '~/components/Header.vue'
  import Footer from '~/components/Footer.vue'
  </script>
  
  <style scoped>
  .content {
    background: white;
    padding: 50px;
    min-height: 280px;
  }
  </style>
  