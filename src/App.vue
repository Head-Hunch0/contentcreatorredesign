<script setup lang="ts">
import Audio from './components/Audio.vue';
import Blob from './components/Blob.vue';
import FAQ from './components/FAQ.vue';
import Features from './components/Features.vue';
import Footer from './components/Footer.vue';
import Hero from './components/Hero.vue';
import LUT from './components/LUT.vue';
import Navbar from './components/Navbar.vue';
import Plugin from './components/Plugin.vue';
import Pricing from './components/Pricing.vue';
import Testimonials from './components/Testimonials.vue';
import Video from './components/Video.vue';



</script>

<template>


  <Navbar class=" bg-gray-900 bg-blur"  />
  <Hero />

  <Features />
  <LUT />
  <Audio />
  <Video />
  <Blob/>
  <Plugin />
  <Testimonials />
  <Pricing />
  <FAQ />
  <Footer />
</template>

