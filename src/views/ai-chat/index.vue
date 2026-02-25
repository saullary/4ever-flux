<script setup lang="ts">
import AiMsg from "./ai-msg.vue";
import aiPrompt from "./ai-prompt.vue";
</script>

<template>
  <div class="">
    <div class="py-4 min-h-[70vh]">
      <ai-msg></ai-msg>
    </div>
    <div class="sticky bottom-0 bg-background z-10">
      <ai-prompt></ai-prompt>
      <div class="py-2 text-center">Powered by 4everland AI</div>
    </div>
  </div>
</template>
