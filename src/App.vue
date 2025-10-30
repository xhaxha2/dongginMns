<script setup lang="ts">
import { RouterView } from 'vue-router'
import MainNav from './components/MainNav.vue'
import SiteFooter from './components/SiteFooter.vue'
</script>
<template>
  <MainNav />
  <RouterView />
  <SiteFooter />
</template>
