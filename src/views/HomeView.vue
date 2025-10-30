<script setup lang="ts">
import ContactSection from '@/components/ContactSection.vue'
import HeroSection from '@/components/HeroSection.vue'
import LicenseGallery from '@/components/LicenseGallery.vue'
import ProjectsSection from '@/components/ProjectsSection.vue'
import ServicesSection from '@/components/ServicesSection.vue'
</script>

<template>
  <main>
    <HeroSection id="page-top" />
    <ServicesSection id="services" />
    <LicenseGallery id="auth" />
    <ProjectsSection id="projects" />
    <ContactSection id="contact" />
  </main>
</template>
