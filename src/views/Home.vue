<script setup lang="ts">
import { useRouter } from "vue-router";
import { Button } from "@/components/ui/button";

const router = useRouter();

const goToDetail = () => {
  router.push("/detail");
};
</script>

<template>
  <div>
    <Button variant="outline" @click="goToDetail">进入详情页</Button>
  </div>
</template>

<style scoped></style>
