<script setup lang="ts">
import { Minus, Plus } from "lucide-vue-next";
import { Button } from "@/components/ui/button";
import {
  Drawer,
  DrawerClose,
  DrawerContent,
  DrawerDescription,
  DrawerFooter,
  DrawerHeader,
  DrawerTitle,
  DrawerTrigger,
} from "@/components/ui/drawer";
import { ref } from "vue";

const goal = ref(350);
</script>

<template>
  <Drawer direction="bottom">
    <DrawerTrigger as-child>
      <Button> Open Drawer </Button>
    </DrawerTrigger>
    <DrawerContent class="mx-auto max-w-lg">
      <div>
        <DrawerHeader>
          <DrawerTitle>Move Goal</DrawerTitle>
          <DrawerDescription>Set your daily activity goal.</DrawerDescription>
        </DrawerHeader>
        <div class="p-4 pb-0">
          <div class="flex items-center justify-center space-x-2">
            <Button
              variant="outline"
              size="icon"
              class="h-8 w-8 shrink-0 rounded-full"
              :disabled="goal <= 200"
              @click="goal -= 10"
            >
              <Minus />
              <span class="sr-only">Decrease</span>
            </Button>
            <div class="flex-1 text-center">
              <div class="text-7xl font-bold tracking-tighter">
                {{ goal }}
              </div>
              <div class="text-muted-foreground text-[0.70rem] uppercase">
                Calories/day
              </div>
            </div>
            <Button
              variant="outline"
              size="icon"
              class="h-8 w-8 shrink-0 rounded-full"
              :disabled="goal >= 400"
              @click="goal += 10"
            >
              <Plus />
              <span class="sr-only">Increase</span>
            </Button>
          </div>
        </div>
        <DrawerFooter>
          <Button>Submit</Button>
          <DrawerClose as-child>
            <Button variant="outline"> Cancel </Button>
          </DrawerClose>
        </DrawerFooter>
      </div>
    </DrawerContent>
  </Drawer>
</template>
