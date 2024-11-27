<script setup lang="ts">
import { ref } from "vue";
import Triangle from "./icons/IconTriangle.vue";
import Scissors from "./icons/IconScissors.vue";
import Rock from "./icons/IconRock.vue";
import Paper from "./icons/IconPaper.vue";
import Options from "@/assets/Options.json";

// Define a reactive variable to store the selected index
const selectedIndex = ref<number | null>(null);

// Function to handle click and set the selected index
const handleSelect = (index: number) => {
  selectedIndex.value = index;
  console.log("Selected index:", index); // Optional: For debugging
};
</script>

<template>
  <div
    class="flex flex-col gap-8 md:flex-row justify-center items-center md:h-full w-full max-w-7xl max-h-[700px]"
  >
    <div
      class="relative w-full h-1/2 md:h-full flex justify-center items-center"
    >
      <Triangle />
      <div
        class="absolute top-1/2 left-1/2 transform -translate-x-1/2 -translate-y-1/2 grid grid-cols-2 gap-12 place-items-center w-60 md:w-72 lg:w-96 h-72 md:h-96"
      >
        <div
          v-for="(option, index) in Options"
          :key="index"
          @click="handleSelect(index)"
          :class="[
            'w-36 h-36 md:w-36 md:h-36 lg:w-44 lg:h-44 flex items-center justify-center absolute',
            index === 0 ? '-top-10 md:top-0 -left-10' : '',
            index === 1 ? '-top-10 md:top-0 -right-10' : '',
            index === 2 ? 'bottom-0' : '',
          ]"
        >
          <div
            class="w-full h-full bg-[#4865f4 absolute top-2 rounded-full"
            :style="{ backgroundColor: option.colorTop }"
          ></div>
          <div
            class="w-full h-full bg-[#5671f5 absolute rounded-full"
            :style="{ backgroundColor: option.colorBottom }"
          ></div>
          <div
            class="w-3/4 h-3/4 bg-slate-300 absolute top-3 mt-2 rounded-full"
          ></div>
          <div class="w-3/4 h-3/4 bg-zinc-200 absolute mt-2 rounded-full"></div>
          <div class="absolute">{{ option.icon }}</div>
        </div>
      </div>
    </div>

    <!-- <div
      class="w-2/3 h-full border-2 border-green-500 flex items-center justify-between"
    >
      <div
        class="text-white font-bold flex flex-col justify-between items-center gap-8"
      >
        <p>YOU PICKED</p>
        <div
          class="w-52 h-52 flex items-center justify-center relative col-span-2"
        >
          <div
            class="w-full h-full bg-[#dc2e4e] absolute top-2 rounded-full"
          ></div>
          <div class="w-full h-full bg-[#dd405d] absolute rounded-full"></div>
          <div
            class="w-3/4 h-3/4 bg-slate-300 absolute top-3 mt-2 rounded-full"
          ></div>
          <div class="w-3/4 h-3/4 bg-zinc-200 absolute mt-2 rounded-full"></div>
          <Scissors class="absolute" />
        </div>
      </div>
      <div class="text-zinc-100 text-4xl font-bold mx-auto md:mx-0">
        <p>YOU WIN</p>
        <button class="bg-white text-red-600 text-sm w-40 h-10 rounded-md">
          PLAY AGAIN
        </button>
      </div>
      <div
        class="text-white font-bold flex flex-col justify-between items-center gap-8"
      >
        <p>YOU PICKED</p>
        <div
          class="w-52 h-52 flex items-center justify-center relative col-span-2"
        >
          <div
            class="w-full h-full bg-[#dc2e4e] absolute top-2 rounded-full"
          ></div>
          <div class="w-full h-full bg-[#dd405d] absolute rounded-full"></div>
          <div
            class="w-3/4 h-3/4 bg-slate-300 absolute top-3 mt-2 rounded-full"
          ></div>
          <div class="w-3/4 h-3/4 bg-zinc-200 absolute mt-2 rounded-full"></div>
          <Scissors class="absolute" />
        </div>
      </div>
    </div> -->
  </div>
</template>
