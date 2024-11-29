<script setup lang="ts">
import { ref } from "vue";
import Logo from "@/components/icons/IconLogo.vue";
import Game from "@/components/Game.vue";
import Rules from "@/components/icons/IconRules.vue";
import Close from "@/components/icons/IconClose.vue";

const rules = ref<boolean>(false);
const gameScore = ref(0);

// Function to update the score
const updateScore = (increment: number) => {
  gameScore.value += increment;
};
</script>

<template>
  <main
    class="w-full min-h-screen max-h-[700px] bg-[#141539] flex flex-col py-3 relative"
  >
    <header>
      <div
        class="w-11/12 md:w-2/3 md:h-36 border-zinc-700 border-2 rounded-lg mx-auto flex justify-between items-center px-5 py-2 max-w-7xl"
      >
        <div class="text-xl md:text-3xl text-zinc-100 font-bold">
          <Logo />
        </div>
        <div
          class="w-24 h-20 md:w-36 md:h-32 bg-zinc-100 rounded-lg flex flex-col justify-center items-center"
        >
          <p>Score</p>
          <p class="text-4xl md:text-7xl">{{ gameScore }}</p>
        </div>
      </div>
    </header>
    <div class="flex justify-center items-center flex-grow pt-10">
      <Game :gameScore="gameScore" :updateScore="updateScore" />
    </div>
    <footer class="self-end">
      <button
        @click="rules = true"
        class="border-2 w-24 flex justify-center items-center h-10 rounded-md mr-5 text-zinc-100 font-bold mt-3 md:mt-0"
      >
        RULES
      </button>
    </footer>
    <div
      v-show="rules"
      class="w-11/12 h-5/6 sm:w-96 sm:h-96 border bg-zinc-200 rounded-md absolute top-1/2 left-1/2 transform -translate-x-1/2 -translate-y-1/2 flex justify-center items-center"
    >
      <div class="relative w-full h-full flex justify-center items-center">
        <Close
          @click="rules = !rules"
          class="absolute right-1 top-1 cursor-pointer"
        />
        <Rules />
      </div>
    </div>
  </main>
</template>
