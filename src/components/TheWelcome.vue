<script setup>
import WelcomeItem from './WelcomeItem.vue'
import DocumentationIcon from './icons/IconDocumentation.vue'

</script>

<template>
  <WelcomeItem>
    <template #icon>
      <DocumentationIcon />
    </template>
    <!-- <template #heading>About</template> -->

    <!-- Vue’s
    <a href="https://vuejs.org/" target="_blank" rel="noopener">official documentation</a>
    provides you with all information you need to get started. -->
  </WelcomeItem>

  <WelcomeItem>
    <video src="../assets/intro.mp4" controls type="video/mp4" autoplay muted loop></video>
  </WelcomeItem>

</template>
