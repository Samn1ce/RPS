<script setup lang="ts">
import Triangle from "./icons/IconTriangle.vue";
import Scissors from "./icons/IconScissors.vue";
import Rock from "./icons/IconRock.vue";
import Paper from "./icons/IconPaper.vue";
import Options from "@/assets/Options.json";
</script>

<template>
  <div
    class="flex justify-center items-center h-full w-full max-w-7xl border-2 border-red-500"
  >
    <div class="relative">
      <Triangle />
      <div
        v-for="(option, index) in Options"
        :key="index"
        class="absolute top-0 grid grid-cols-2 gap-12"
      >
        <div
          :class="[
            'w-44 h-44 flex items-center justify-center -top-20  relative',
            index === 1 ? '-right-5' : '',
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
    <!-- 
       -->
    <!-- <div
          class="w-44 h-44 flex items-center justify-center -top-20 -right-5 relative"
        >
          <div
            class="w-full h-full bg-[#ec9e0e] absolute top-2 rounded-full"
          ></div>
          <div class="w-full h-full bg-[#eca922] absolute rounded-full"></div>
          <div
            class="w-3/4 h-3/4 bg-slate-300 absolute top-3 mt-2 rounded-full"
          ></div>
          <div class="w-3/4 h-3/4 bg-zinc-200 absolute mt-2 rounded-full"></div>
          <Scissors class="absolute" />
        </div> -->
    <!-- 
       -->
    <!-- <div
          class="w-44 h-44 flex items-center justify-center relative col-span-2 justify-self-center bottom-24"
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
      <div class="text-zinc-100 text-4xl font-bold">
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
